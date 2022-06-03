<template>
  <!-- component that shows a value as average of bitstamp, coinbase and bitfinex-->
  <div class="gj-avg-ticker-values">
    {{ average }} $
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "GJAvgTickerValues",
  data() {
    return {
      bitstamp: 0,
      coinbase: 0,
      bitfinex: 0
    };
  },
  computed: {
    average() {
      return (
        (this.bitstamp + this.coinbase + this.bitfinex) / 3
      ).toFixed(2);
    }
  },
  mounted() {
    axios.defaults.headers['Access-Control-Allow-Origin'] = '*';
    // get the data from bitstamp api
    axios.get("https://www.bitstamp.net/api/v2/ticker/btcusd/")
        .then(
            response => {
            this.bitstamp = response.data.last;})
        .catch(
            error => {
              console.log("error in bitstamp");
            console.log(error);
            });
    // get the data from coinbase api
    axios.get("https://api.coinbase.com/v2/exchange-rates?currency=BTC")
        .then(
            response => {
            this.coinbase = response.data.data.rates.USD;})
        .catch(
            error => {
              console.log("error in coinbase")
              console.log(error);
            });
    // get the data from bitfinex api
    axios.get("https://api-pub.bitfinex.com/v2/tickers?symbols=tBTCUSD")
        .then(
            response => {
            this.bitfinex = response.data[0][1];})
        .catch(
            error => {
              console.log("error in bitfinex")
              console.log(error);
            });
  }
}
</script>

<style scoped>
/* class gj-avg-ticker-values has a green background and rounded corners, it floats left,
text align is at the center*/
.gj-avg-ticker-values {
  background-color: #2ecc71;
  border-radius: 5px;
  float: left;
  margin-right: 10px;
  padding: 10px;
  width: 100%;
  text-align: center;
  vertical-align: center;
}
</style>