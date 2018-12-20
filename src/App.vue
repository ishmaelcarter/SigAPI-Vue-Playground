<template>
  <div id="app">
  <div>
      <img src="https://upload.wikimedia.org/wikipedia/commons/3/3e/Dollar_sign_in_circle.svg">
        {{ btc }}
      <img width="50px" src="https://en.bitcoin.it/w/images/en/6/69/Btc-sans.png">
    </div>
    <div>
      <img src="https://upload.wikimedia.org/wikipedia/commons/3/3e/Dollar_sign_in_circle.svg">
        {{ eth }}
      <img width="50px" src="https://www.ethereum.org/images/logos/ETHEREUM-ICON_Black_small.png">
    </div>
    <div>
      <img width="50px"src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Euro_symbol_black.svg">
      {{ eur_btc }}
      <img width="50px" src="https://en.bitcoin.it/w/images/en/6/69/Btc-sans.png">
    </div>
    <div>
      <img width="50px"src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Euro_symbol_black.svg">
      {{ eur_eth }}
      <img width="50px" src="https://www.ethereum.org/images/logos/ETHEREUM-ICON_Black_small.png">
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'
export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data () {
    return {
      btc: null,
      eth: null,
      eur_btc: null,
      eur_eth: null,
      api_key: API_KEY
    }
  },
  mounted () {
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/BTC/USD?apikey={{api_key}}")
      .then(response => (this.btc = response.data.rate)),
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/ETH/USD?apikey={{api_key}}")
      .then(response => (this.eth = response.data.rate))
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/BTC/EUR?apikey={{api_key}}")
      .then(response => (this.eur_btc = response.data.rate)),
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/ETH/EUR?apikey={{api_key}}")
      .then(response => (this.eur_eth = response.data.rate))
  }
  }

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
