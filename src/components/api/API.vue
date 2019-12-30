<template>
  <div>
    {{info}}
    <h1>Bitcoin Price Index</h1>
    <div v-bind:key="currency.code" v-for="currency in info">
      {{currency.description}}:
      <span v-html="currency.symbol"></span>
      {{currency.rate_float | currencydecimal}}
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "API",
  data() {
    return {
      info: null
    };
  },
  mounted() {
    axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then(response => (this.info = response.data.bpi))
      .catch(error => {
          console.log(error)
          this.errored = true
      })
      .finally(() => this.loading = false)

    // fetch('https://api.coindesk.com/v1/bpi/currentprice.json', {mode:'cors'})
    // .then(function(response){
    //     return response.text();
    // })
    // .then(function(text){
    //     console.log('Request successful', text);
    // })
    // .catch(function(error){
    //     console.log('Request failed', error)
    // });
  },
  filters: {
    currencydecimal(value) {
      return value.toFixed(2);
    }
  }
};
</script>