<template>
  <div class="container">
    <div class="header row">
      <h2 class="col-12 col-md-10">Check Your Currency</h2>
      <select v-model="currency" class="form-control col-12 col-md-2">
        <option value="usd" default>USD</option>
        <option value="eur">EUR</option>
      </select>
    </div>
    <div class="row border-bottom" v-for="(value, key) in cryptos" v-bind:key="key">
      <div class="crypto-key col">
        <p>{{key}}</p>
      </div>
      <div class="crypto-currency col" v-if="currency === 'usd'">
        <p>${{value.USD}}</p>
      </div>
      <div class="crypto-currency col" v-else>
        <p>€{{value.EUR}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app-crypto',
  data: () => ({
    cryptos: [],
    errors: [],
    currency: 'usd'
  }),
  created () {
    axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,IOT&tsyms=USD,EUR')
      .then(response => {
        this.cryptos = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .header {
    margin-top: 1.5rem;
    margin-bottom: 1.5rem;
    padding: 0 .5rem;
  }
  select {
    margin: 0.5rem 0 1rem;
  }
  p {
    margin-bottom: 0.25rem;
  }
  .crypto-key {
    padding: 1rem;
  }
  .crypto-currency {
    padding: 1rem;
    display: flex;
    justify-content: flex-end;
  }
</style>
