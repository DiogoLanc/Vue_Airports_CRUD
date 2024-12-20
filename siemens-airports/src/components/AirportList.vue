<template>
    <div>
      <h2>Airport List</h2>
      <ul>
        <li v-for="(airport, index) in airports" :key="index">
          {{ airport.iata }} - {{ airport.name }}
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      airports: Array,
    }
  };
  </script>
  