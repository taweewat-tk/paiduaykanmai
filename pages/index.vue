<template>
  <div>
    <div class="text-center bold">
      Form and Validation
    </div>
    <div class="d-flex justify-content-center">
      <b-form class="col-6" @submit.stop.prevent="onSubmit">
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

        <b-button type="submit" variant="primary">
          Submit
        </b-button>
      </b-form>
    </div>
    <div v-if="showResult" class="d-flex justify-content-center pt-4">
      <div class="col-6">
        <b>Result:</b>
        <div>
          First Name : {{ form.firstname }}
        </div>
        <div>
          Last Name : {{ form.lastname }}
        </div>
        <div>
          E-mail : {{ form.email }}
        </div>
        <div>
          Gender : {{ form.gender }}
        </div>
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
      email: {
        required,
        email
      },
      password: {
        required
      },
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
      this.showResult = true
    }
  }
}
</script>

<style>

</style>
