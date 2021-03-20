<template>
  <div>
    <div class="row card-custom card-shadow p-4">
      <div v-if="showResult" class="col-8 vertical-middle">
        <!-- Result -->
        <div class="vc">
          <div class="pr-3">
            <img src="~/assets/images/user-96.png" width="90px">
          </div>
          <div>
            <div class="text-name">
              {{ preview.firstname }} {{ preview.lastname }}
            </div>
            <div class="vc">
              <img src="~/assets/images/mail-24.png" class="mr-1" width="18px">
              {{ preview.email }}
              <img src="~/assets/images/user-48.png" class="mr-1 ml-4" width="18px">
              {{ preview.gender }}
            </div>
          </div>
        </div>
      </div>
      <div v-if="!showResult" class="col-8 vertical-middle">
        <img src="~/assets/images/index.jpg" width="500px">
      </div>
      <div class="col-4">
        <b-form @submit.stop.prevent="onSubmit">
          <div class="text-center bold pb-3">
            Form and Validation
          </div>
          <b-form-group id="input-group-firstname" label="First Name" label-for="firstname">
            <b-form-input
              id="firstname"
              v-model="$v.form.firstname.$model"
              name="firstname"
              :state="validateState('firstname')"
              aria-describedby="input-firstname"
            />
            <b-form-invalid-feedback
              id="input-firstname"
            >
              This is a required field.
            </b-form-invalid-feedback>
          </b-form-group>

          <b-form-group id="input-group-lastname" label="Last Name" label-for="lastname">
            <b-form-input
              id="lastname"
              v-model="$v.form.lastname.$model"
              name="lastname"
              :state="validateState('lastname')"
              aria-describedby="input-lastname"
            />
            <b-form-invalid-feedback
              id="input-lastname"
            >
              This is a required field.
            </b-form-invalid-feedback>
          </b-form-group>

          <b-form-group id="input-group-email" label="E-mail" label-for="email">
            <b-form-input
              id="email"
              v-model="$v.form.email.$model"
              name="email"
              :state="validateState('email')"
              aria-describedby="input-email"
            />
            <b-form-invalid-feedback
              id="input-email"
            >
              This is a required field and must be an email.
            </b-form-invalid-feedback>
          </b-form-group>

          <b-form-group id="input-group-password" label="Password" label-for="password">
            <b-form-input
              id="password"
              v-model="$v.form.password.$model"
              type="password"
              name="password"
              :state="validateState('password')"
              aria-describedby="input-password"
            />
            <b-form-invalid-feedback
              id="input-password"
            >
              This is a required field.
            </b-form-invalid-feedback>
          </b-form-group>

          <b-form-group id="input-group-verifyPassword" label="Verify Password" label-for="verifyPassword">
            <b-form-input
              id="verifyPassword"
              v-model="$v.form.verifyPassword.$model"
              type="password"
              name="verifyPassword"
              :state="validateState('verifyPassword')"
              aria-describedby="input-verifyPassword"
            />
            <b-form-invalid-feedback
              id="input-verifyPassword"
            >
              This is a required field and passwords must be identical.
            </b-form-invalid-feedback>
          </b-form-group>

          <b-form-group id="input-group-gender" label="Gender" label-for="gender">
            <b-form-select
              id="input-gender"
              v-model="$v.form.gender.$model"
              name="gender"
              :options="gender"
              :state="validateState('gender')"
              aria-describedby="input-gender"
            />
            <b-form-invalid-feedback
              id="input-gender"
            >
              This is a required field.
            </b-form-invalid-feedback>
          </b-form-group>

          <div class="d-flex justify-content-center pt-3">
            <b-button type="submit" variant="success" class="btn-block btn-submit">
              Submit
            </b-button>
          </div>
        </b-form>
      </div>
    </div>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, sameAs, email } from 'vuelidate/lib/validators'
export default {
  mixins: [validationMixin],
  data () {
    return {
      showResult: false,
      gender: [
        { text: 'Please select a gender', value: null },
        { text: 'Male', value: 'Male' },
        { text: 'Female', value: 'Female' }
      ],
      form: {
        firstname: null,
        lastname: null,
        email: null,
        password: null,
        verifyPassword: null,
        gender: null
      },
      preview: {
        firstname: null,
        lastname: null,
        email: null,
        gender: null
      }
    }
  },
  validations: {
    form: {
      firstname: {
        required
      },
      lastname: {
        required
      },
      // email input must be format test@test.com
      email: {
        required,
        email
      },
      password: {
        required
      },
      // verifyPassword input must be same as password input
      verifyPassword: {
        required,
        sameAsPassword: sameAs('password')
      },
      gender: {
        required
      }
    }
  },
  methods: {
    validateState (name) {
      const { $dirty, $error } = this.$v.form[name]
      return $dirty ? !$error : null
    },
    onSubmit () {
      this.$v.form.$touch()
      if (this.$v.form.$anyError) {
        return
      }

      this.preview.firstname = this.form.firstname
      this.preview.lastname = this.form.lastname
      this.preview.email = this.form.email
      this.preview.gender = this.form.gender
      this.showResult = true
    }
  }
}
</script>

<style>
  .text-name{
    font-size: 32px;
    font-weight: bold;
  }
  img{
    opacity: 0.9;
  }
</style>
