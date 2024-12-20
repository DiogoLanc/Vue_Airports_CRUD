<template>
    <div>
      <h2>Airport List</h2>
      <ul>
        <li v-for="(airport, index) in airports" :key="index">
           {{ airport.iata }} - {{ airport.name }}
          <button v-on:click="deleteAirport(index)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
    export default {
        props: {
            airports: Array,
        },
        methods: {
            deleteAirport(index) {
            this.$emit("delete-airport", index);
            },
        },
    };
  </script>
  