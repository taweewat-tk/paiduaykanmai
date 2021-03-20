<template>
  <div class="row justify-content-lg-center">
    <div class="col-6 card-custom card-shadow p-4">
      <div class="text-center bold pb-3">
        Function 2
      </div>
      <div>
        Full datetime : <b>{{ fullDateTime }}</b>
      </div>
      <div>
        Thai format datetime : <b>{{ thaiDateTime }}</b>
      </div>
      <div>
        The number of days in this month : <b>{{ dayInThisMonth }}</b>
      </div>
      <div>
        This quarter of the month : <b>{{ quarterByMonth }}</b>
      </div>
      <div>
        Unix timestamp : <b>{{ unixTimeStamp }}</b>
      </div>
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
    dayInThisMonth () {
      return this.formatDaysInMonth(this.date)
    },
    quarterByMonth () {
      return this.formatQuarterByMonth(this.date)
    },
    unixTimeStamp () {
      return this.formatUnixTimeStamp(this.date)
    },
    thaiDateTime () {
      return this.formatThaiDateTime(this.date)
    }
  },
  methods: {
    // format datetime ex.10/08/2020 14:54
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
    // Thai datetime format ex. 10 สิงหาคม 2563
    formatThaiDateTime (date) {
      const newDate = new Date(date)
      const year = newDate.getFullYear() + 543
      const monthsTH = ['มกราคม', 'กุมภาพันธ์', 'มีนาคม', 'เมษายน', 'พฤษภาคม', 'มิถุนายน', 'กรกฎาคม', 'สิงหาคม', 'กันยายน', 'ตุลาคม', 'พฤศจิกายน', 'ธันวาคม']
      const month = ('00' + (newDate.getMonth() + 1)).slice(-2)
      const dateStr =
        ('00' + newDate.getDate()).slice(-2) + ' ' +
        monthsTH[Number(month) - 1] + ' ' + year
      return dateStr
    },
    // days inmonth
    formatDaysInMonth (date) {
      const newDate = new Date(date)
      const year = newDate.getFullYear()
      const month = ('00' + (newDate.getMonth() + 1)).slice(-2)
      return new Date(year, Number(month), 0).getDate()
    },
    // Quarter
    formatQuarterByMonth (date) {
      const newDate = new Date(date)
      const month = ('00' + (newDate.getMonth() + 1)).slice(-2)
      return Math.floor((Number(month) - 1) / 3) + 1
    },
    // Unix timestamp
    formatUnixTimeStamp (date) {
      const newDate = new Date(date)
      return Math.round(newDate.getTime() / 1000.0)
    }
  }
}
</script>
