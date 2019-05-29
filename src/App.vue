<template>
  <div id="app">
  <button v-on:click="GET_AGENTS">get all agents</button>
  <div v-if="Array.isArray(agents)">
    <div v-for="agent in agents" :key="agent.id">
      <div v-if="agent.title">
        <a class="link" :href="agent.link">{{agent.title.rendered}}</a>
        <img :href="agent._links['wp:attachment']['0'].href">
      </div>
    </div>
  </div>
    <div>
        <button v-on:click="SEARCH_ALL">
        get {{ this.offer_type }} offers
      </button>
    </div>
    <div v-if="offer_type == 'cruise'">
      <label value="Supplier ID">Cruise Supplier: </label>
      <select type="text" name="supplier" list="suppliername" v-model="supplier_id">
        <option value="586">Oceania</option>
        <option value="29">Regent</option>
        <option value="26">Silversea</option>
      </select>
    </div>
    <div>
      <label value="Supplier ID">Offer Type: </label>
      <select type="text" name="offer" list="offertype" v-model.lazy="offer_type">
        <option value="cruise">Cruise</option>
        <option value="tour">Tour</option>
        <option value="hotel">Hotel</option>
      </select>
    </div>
    <div v-if="offer_type == 'cruise'">
      <h2>Cruise Search</h2>
      <div v-for="offer in offers" :key="offer.id">
        <div class="offers" v-if="offer.title">
          <p class="title">{{ offer.title }}</p>
          <p class="itinerary">{{ offer.itinerary_description }}</p>
          <p class="depart">{{ offer.depart_day.replace('T00:00:00','') }}</p>
          <p class="description">{{ offer.available_addons.replace(/&lt;[^>]+>/g, '') }}</p>
          <p><a class="link" :href="offer.offer_link">See Offer</a></p>
        </div>
      </div>
    </div>
    <div v-if="offer_type == 'hotel'">
      <h2>Hotel Search</h2>
      <div v-for="offer in offers" :key="offer.id">
        <div class="offers" v-if="offer.title">
          <p class="title">{{ offer.title }}</p>
          <p class="itinerary">{{ offer.itinerary_description }}</p>
          <p><a class="link" :href="offer.offer_link">See Offer</a></p>
        </div>
      </div>
    </div>
    <div v-if="offer_type == 'tour'">
      <h2>Tour Search</h2>
      <div v-for="offer in offers" :key="offer.id">
        <div class="offers" v-if="offer.title">
          <p class="title">{{ offer.title }}</p>
          <p class="depart">{{ offer.drop_day.replace('T00:00:00','') }}</p>
          <p class="itinerary">{{ offer.itinerary_description }}</p>
          <p><a class="link" :href="offer.offer_link">See Offer</a></p>
        </div>
      </div>
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
      offers: "No Offers to Show",
      supplier_id: "0",
      url: "https://api.signaturetravelnetwork.com/sws/v1/offers",
      offer_type: "cruise",
      agents: "No Agents to Show"
    }
  },
  mounted () {

  },
  methods: {
    SEARCH_ALL: function(){
    axios
      .get(this.url + "/" + this.offer_type + "/?max_return=200", {
        params: {
          api_key: process.env.VUE_APP_API_KEY
        }
      })
      .then(response => (this.offers = response.data.offers))
      .catch(error => (this.offers = error))
    },
    GET_AGENTS: function(){
      axios
        .get("http://bvtravel.com/wp-json/wp/v2/advisor", {

        })
        .then(response => (this.agents = response.data))
        .catch(error => (this.agents = error))
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
  border-radius: 3%;
  width: 100%;
  padding: 0;
  margin: auto;
  margin-bottom: 1%;
}

div button {
  width: 12.5%;
  padding: 1% 0;
  font-size: 100%;
  margin: auto;
  align-items: center;
  justify-content: space-between;
  text-align: center;
  background: linear-gradient(to left,#7CBB91,#4E9C68,#7CBB91);
  border-radius: 3%;
  text-transform: uppercase;
}

div button img {
  display:inline-block;
  margin:auto;
  height:100%;
}

div p {
  font-size: 100%;
  font-weight: bold;
}

.offers {
  border: 1px solid black;
  display: flex;
}

.offers p{
  padding: 0 .5%;
}
</style>
