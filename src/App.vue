<template>
  <div id="app">
    <div id="title">ESTIMATION TOOL</div>
    <div id="entry">
      <div id="description">Number of Families (on an <b>Average</b> a family would consist of <b>5 members</b>)</div>
      <input type="number" v-model="text" class="form-control" aria-label="Small" aria-describedby="inputGroup-sizing-sm">
      <button type="button" class="btn btn-primary" v-on:click="showResult()">Submit</button>
    </div>
    <div id="result">
      <div id="sub-title">Estimated Amount</div>
      <div id="description">Total Amount ( Number of families * Monthly package amount) = <b>{{totalAmount}}</b> for {{numberOfFamilies}} families</div>
      <div id="sub-description">This is an estimated amount and not the actual, actual price may slightly vary.</div>
      <div id="table">
        <div id="table-description">Monthly Consumption Expenses of Essential Commodities (For a family of 4-5 members)</div>
        <b-table bordered hover :items="tableItems"></b-table>
      </div>
    </div>
  </div>
</template>

<script>
// Canonical data - modify this to make changes to the webpage.
const _items = [
  // Item, Quantity, Unit of Measurement, Price Per Unit
  ['Rice', 12, 'KG', 65],
  ['Ragi', 5, 'KG', 25],
  ['Wheat Flour', 5, 'KG', 50],
  ['Oil', 5, 'Liter', 100],
  ['Sugar', 3, 'KG', 55],
  ['Salt', 1, 'KG', 18],
  ['Onion', 4, 'KG', 40],
  ['Potatoes', 4, 'KG', 30],
  ['Toor Dal', 2, 'KG', 60],
  ['Urad Dal', 1, 'KG', 120]
]

function _formatINR (number) {
  const roundedUp = Math.ceil(number / 10) * 10
  const formatted = new Intl.NumberFormat(
    'en-IN',
    {
      style: 'currency',
      currency: 'INR'
    }
  ).format(roundedUp)
  return formatted.replace('.00', '')
}

function calcuatePackageCost (numFamilies) {
  var cost = 0
  _items.forEach(item => {
    cost += (item[1] * item[3])
  })
  cost += (cost * 0.05) // Add 5% transportation cost
  const totalCost = cost * numFamilies
  return _formatINR(totalCost)
}

function getTableData () {
  const ret = JSON.parse(JSON.stringify(_items)) // Deep copy
  ret.push(['Contingency & travels (5%)', null, null, null])
  return ret
}

export default {
  data () {
    return {
      text: '',
      totalAmount: '₹ 0',
      numberOfFamilies: 0,
      tableData: '',
      tableItems: ''
    }
  },
  methods: {
    showResult: function () {
      this.numberOfFamilies = this.text
      if (this.numberOfFamilies === '') {
        this.numberOfFamilies = '0'
      }
      this.totalAmount = calcuatePackageCost(this.numberOfFamilies)
    },
    renderTableData () {
      var tableRows = getTableData()
      var rows = []
      for (var i = 0; i < tableRows.length; i++) {
        rows.push({Items: tableRows[i][0], Quantity: tableRows[i][1], Unit_Of_Measurement: tableRows[i][2]})
      }
      return rows
    }
  },
  created () {
    this.tableItems = this.renderTableData()
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
  font-style: normal;
  line-height: 28px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 92px;
  margin-left: 90px;
}
#title {
  font-size: 24px;
  font-weight: bold;
}
#description {
  font-size: 16px;
  line-height: 24px;
  margin-top: 25px;
}
.form-control {
  margin-top: 10px;
  max-width: 550px;
}
.btn {
  margin-top: 20px;
}
#sub-title {
  margin-top: 50px;
  font-weight: 500;
  font-size: 24px;
  line-height: 26px;
}
#sub-description {
  font-size: 13px;
  line-height: 19px;
  color: #818A91;
}
#table-description {
  font-size: 14px;
  line-height: 21px;
  margin-top: 50px;
}
.table {
  max-width: 550px;
}
</style>
