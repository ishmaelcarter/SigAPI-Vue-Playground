<template>
  <div id="app">
    <div>
    {{api_key}}
      <button @click="USD_BTC">
        <img src="https://upload.wikimedia.org/wikipedia/commons/3/3e/Dollar_sign_in_circle.svg">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Chevron_right_font_awesome.svg">
        <img width="50px" src="https://en.bitcoin.it/w/images/en/6/69/Btc-sans.png">
      </button>
      <p>{{ btc }}</p>
    </div>
    <div>
      <button @click="USD_ETH">
        <img src="https://upload.wikimedia.org/wikipedia/commons/3/3e/Dollar_sign_in_circle.svg">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Chevron_right_font_awesome.svg">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/0/05/Ethereum_logo_2014.svg">
      </button>
      <p>{{ eth }}</p>
    </div>
    <div>
      <button @click="EUR_BTC">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Euro_symbol_black.svg">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Chevron_right_font_awesome.svg">
        <img width="50px" src="https://en.bitcoin.it/w/images/en/6/69/Btc-sans.png">
      </button>
      <p>{{ eur_btc }}</p>
    </div>
    <div>
      <button @click="EUR_ETH">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Euro_symbol_black.svg">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Chevron_right_font_awesome.svg">
        <img width="50px" src="https://upload.wikimedia.org/wikipedia/commons/0/05/Ethereum_logo_2014.svg">
      </button>
      <p>{{ eur_eth }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
require('dotenv').config()
export default {
  name: 'app',
  components: {

  },
  data () {
    return {
      btc: null,
      eth: null,
      eur_btc: null,
      eur_eth: null
    }
  },
  methods: {
    USD_BTC: function(){
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/BTC/USD?apikey=" + process.env.VUE_APP_API_KEY)
      .then(response => (this.btc = response.data.rate))
    },
    USD_ETH: function(){
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/ETH/USD?apikey=" + process.env.VUE_APP_API_KEY)
      .then(response => (this.eth = response.data.rate))
    },
    EUR_BTC: function(){
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/BTC/EUR?apikey=" + process.env.VUE_APP_API_KEY)
      .then(response => (this.eur_btc = response.data.rate))
    },
    EUR_ETH: function(){
    axios
      .get("https://rest.coinapi.io/v1/exchangerate/ETH/EUR?apikey=" + process.env.VUE_APP_API_KEY)
      .then(response => (this.eur_eth = response.data.rate))
    }
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

#app div {
  border: 3px solid #105D2A;
  border-radius: 3%;
  width: 25%;
  padding: 0;
  margin: auto;
  margin-bottom: 1%;
}

div button {
  display: flex;
  width: 100%;
  margin: auto;
  align-items: center;
  justify-content: space-between;
  background: linear-gradient(to left,#7CBB91,#4E9C68,#7CBB91);
  border-radius: 3%;
}

div button img {
  display:inline-block;
  margin:auto;
  height:100%;
}

div p {
  font-size: 200%;
  font-weight: bold;
}
</style>
