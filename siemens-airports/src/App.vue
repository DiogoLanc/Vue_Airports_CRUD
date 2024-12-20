<template>
  <div id="app">
    <h1 class = "tittle">Airport Manager - Control and Manage Your Airports</h1>
    <AirportForm v-on:add-airport="addAirport" />
    <AirportList :airports="airports" 
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

    // adicionar aeroporto
    addAirport(newAirport) {
      this.airports.push(newAirport);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    },

    // apagar aeroporto
    deleteAirport(index) {
      this.airports.splice(index, 1);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    },

    // atualizar aeroporto 
    updateAirport(index, updatedAirport) {
      this.airports.splice(index, 1, updatedAirport);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    },
  },
};
</script>

<style scoped>
  #app {
    background-color: #e4e4e4; 
    color: black; 
  }

</style>
