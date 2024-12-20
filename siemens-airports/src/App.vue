<template>
  <div id="app">
    <h1 class = "tittle">Airport Manager - Control and Manage Your Airports</h1>
    <AirportForm v-on:add-airport="addAirport" />
    <AirportList :airports="airports" v-on:delete-airport="deleteAirport" />
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
    addAirport(newAirport) {
      this.airports.push(newAirport);
      localStorage.setItem("airports", JSON.stringify(this.airports));
      console.log("Airport added:", newAirport);
    },

    deleteAirport(index) {
      this.airports.splice(index, 1);
      localStorage.setItem("airports", JSON.stringify(this.airports));
    }
  },
};
</script>

<style scoped>
  #app {
    background-color: #e4e4e4; /* Example solid background color */
    color: black; /* Adjust text color */
  }

</style>
