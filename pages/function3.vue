<template>
  <div>
    <div class="d-flex justify-content-center">
      <b-form class="col-7 card-custom card-shadow p-4" @submit.stop.prevent="onSubmit">
        <div class="text-center bold pb-3">
          Function 3
        </div>
        <b-form-group id="input-group-arrNumber" label="Input array of numbers (only numbers,comma and ,, = 0)" label-for="arrNumber">
          <b-form-input
            id="arrNumber"
            v-model="form.strNumber"
            name="arrNumber"
            placeholder="1,2,3,4,5,6,7"
            @keydown="onKeyDown"
          />
        </b-form-group>
        <b-button type="submit" variant="success" class="btn-submit btn-block">
          Check
        </b-button>
        <div class="bold pt-4">
          Second max number is {{ getSecondMax }}
        </div>
        <div>
          Sorted array is {{ arrSort }}
        </div>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      form: {
        strNumber: null
      },
      arrNumber: [],
      arrSort: null
    }
  },
  computed: {
    getSecondMax () {
      return this.secondMax(this.arrNumber)
    }
  },
  methods: {
    onSubmit () {
      if (this.form.strNumber) {
        this.arrNumber = (this.form.strNumber).split(',')
      } else {
        this.arrNumber = null
        this.arrSort = '[]'
      }
    },
    // only input number and comma
    onKeyDown (e) {
      if (
        e.key !== 'Tab' &&
        e.key !== 'Backspace' &&
        e.key !== 'ArrowLeft' &&
        e.key !== 'ArrowRight' &&
        e.key !== '0' &&
        e.key !== '1' &&
        e.key !== '2' &&
        e.key !== '3' &&
        e.key !== '4' &&
        e.key !== '5' &&
        e.key !== '6' &&
        e.key !== '7' &&
        e.key !== '8' &&
        e.key !== '9' &&
        e.key !== ','
      ) {
        e.preventDefault()
      }
    },
    secondMax (arr) {
      let secondMax = null
      if (arr) {
        arr = this.convertStringArrToNumberArr(arr)
        arr = this.sortArr(arr)
        this.arrSort = '[' + arr.toString() + ']'
        const uniqArr = [...new Set(arr)]
        arr = uniqArr

        if (arr[arr.length - 2] != null) {
          // second max number
          secondMax = arr[arr.length - 2]
          return secondMax
        } else if (arr[arr.length - 1] != null) {
          // condition for array length is 1
          secondMax = arr[arr.length - 1]
          return secondMax
        } else {
          secondMax = null
          return secondMax
        }
      }
      return secondMax
    },
    // for sort number of array
    sortArr (arr) {
      return arr.sort((a, b) => a - b)
    },
    // for convert to number ex. 00001 to 1
    convertStringArrToNumberArr (arr) {
      return arr.map(Number)
    }
  }
}
</script>
