<template>
  <div id="app">
    <h1 class = "tittle">Airport Manager - Control and Manage Your Airports</h1>
    <AirportForm v-on:add-airport="addAirport" />
  </div>
</template>

<script>
import AirportForm from "./components/AirportForm.vue";

export default {
  components: { AirportForm },
  data() {
    return {
      airports: [],
    };
  },
  methods: {
    addAirport(newAirport) {
      this.airports.push(newAirport);
      console.log("Airport added:", newAirport);
    },
  },
};
</script>

<style scoped>
.tittle {
  font-weight: bold;
  text-align: center;
  margin-bottom: 30px;
}
</style>
