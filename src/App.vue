<template>
  <div id="app">
    <div id="title">ESTIMATION TOOL</div>
    <div id="entry">
      <div id="description">Number of Families (on an <b>Average</b> a family would consist of <b>5 members</b>)</div>
      <input type="text" v-model="text" class="form-control" aria-label="Small" aria-describedby="inputGroup-sizing-sm">
      <button type="button" class="btn btn-primary" v-on:click="result(3)">Submit</button>
    </div>
    <div id="result">
      <div id="sub-title">Estimatied Amount</div>
      <div id="description">Total Amount ( Number of families * Monthly pakage amount) = INR 54000 for 3 families</div>
      <div id="sub-description">This is an estimated amount and not the actual, actual price may slightly vary.</div>
      <div id="table">
        <div id="table-description">Monthly Consumption Expenses of Essential Commodities (For a family of 4-5 members)</div>
        <table class="table table-bordered">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Items</th>
              <th scope="col">Quantity</th>
              <th scope="col">Unit of Measurement</th>
            </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      text: ''
    }
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
