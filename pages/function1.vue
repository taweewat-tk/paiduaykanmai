<template>
  <div>
    <div class="d-flex justify-content-center">
      <div class="col-sm-6 card-custom card-shadow p-4">
        <div class="text-center bold pb-3">
          Function 1
        </div>
        <div>
          <b-table :items="summaryData" class="text-center table-bordered" outlined />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import examData from '~/static/exam-data.json'
export default {
  data () {
    return {
      dataList: examData,
      summaryData: []
    }
  },
  created () {
    this.findProductsWeight()
  },
  methods: {
    // get name and calculate weight of products
    findProductsWeight () {
      this.dataList.forEach((data) => {
        if (data.is_editable_price === false) {
          const productObj = {
            name: data.name,
            totalSubProductWeight: 0
          }
          data.products.forEach((product) => {
            productObj.totalSubProductWeight += product.weight
          })
          this.summaryData.push(productObj)
        }
      })
    }
  }
}
</script>

<style>
thead{
  background:#1ABC9C;
  color:#FFFFFF
}
table{
  border-radius: 20px;
}
</style>
