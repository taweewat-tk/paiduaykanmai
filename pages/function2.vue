<template>
  <div>
    <div class="text-center bold pb-3">
      Function 2
    </div>
    <div>
      Full Datetime : {{ fullDateTime }}
    </div>
    <div>
      Days : {{ day }}
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      date: '2020-08-10T14:54:52+07:00'
    }
  },
  computed: {
    fullDateTime () {
      return this.formatDateTime(this.date)
    },
    day () {
      return this.formatDay(this.date)
    }
  },
  methods: {
    formatDateTime (date) {
      const newDate = new Date(date)
      const year = newDate.getFullYear()
      const dateStr =
        ('00' + newDate.getDate()).slice(-2) + '/' +
        ('00' + (newDate.getMonth() + 1)).slice(-2) + '/' + year + ' ' +
        ('00' + newDate.getHours()).slice(-2) + ':' +
        ('00' + newDate.getMinutes()).slice(-2)
      return dateStr
    },
    formatDay (date) {
      const newDate = new Date(date)
      const day = newDate.getDay()
      return day
    }
  }
}
</script>
