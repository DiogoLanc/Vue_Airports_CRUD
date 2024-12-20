<template>
  <div id="app">
    <h1 class="tittle">Airport Manager</h1>
    <AirportForm v-on:add-airport="addAirport" />
    <AirportList v-bind:airports="airports" 
                  v-on:delete-airport="deleteAirport" 
                  v-on:update-airport="updateAirport"
    />
  </div>
</template>

<script>
import AirportForm from "./components/AirportForm.vue";
import AirportList from "./components/AirportList.vue";

export default {
  components: { AirportForm, AirportList },
  data() {
    return {
      airports: JSON.parse(localStorage.getItem("airports")) || [],
    };
  },

  methods: {

    // add Airport
    addAirport(newAirport) {
      this.airports.push(newAirport);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    },

    // delete Airport
    deleteAirport(index) {
      this.airports.splice(index, 1);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    },

    // update Airport 
    updateAirport(index, updatedAirport) {
      this.airports.splice(index, 1, updatedAirport);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    },
  },
};
</script>

<style scoped>

  #app {
    background-color: #c9c9c97e; 
    color: black; 
  }

  .tittle {
    text-align: center; 
  }

</style>
