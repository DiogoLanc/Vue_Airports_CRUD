<template>
  <div>
    <h2>Airport List</h2>
    <ul>
      <li v-for="(airport, index) in airports" :key="index">
        <div v-if="editingIndex === index">
          <input
            v-model="editingIata"
            maxlength="3"
            placeholder="IATA Code"
            v-on:input="convertToUppercase"
          />
          <input v-model="editingName" placeholder="Airport Name" />
          <button v-on:click="saveEdit(index)">Save</button>
          <button v-on:click="cancelEdit">Cancel</button>
        </div>
        <div v-else>
          {{ airport.iata }} - {{ airport.name }}
          <button v-on:click="editAirport(index, airport)">Edit</button>
          <button v-on:click="deleteAirport(index)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    airports: Array,
  },
  data() {
    return {
      editingIndex: null, 
      editingIata: "",
      editingName: "",
    };
  },
  methods: {
    deleteAirport(index) {
      this.$emit("delete-airport", index);
    },
    editAirport(index, airport) {
      this.editingIndex = index;
      this.editingIata = airport.iata;
      this.editingName = airport.name;
    },
    saveEdit(index) {
      if (!this.editingIata.match(/^[A-Z]{3}$/)) {
        alert("IATA code must be 3 uppercase letters.");
        return;
      }
      if (this.editingName.trim() === "") {
        alert("Airport name is required.");
        return;
      }
      const updatedAirport = { iata: this.editingIata, name: this.editingName };
      this.$emit("update-airport", index, updatedAirport);
      this.cancelEdit();
    },
    cancelEdit() {
      this.editingIndex = null;
      this.editingIata = "";
      this.editingName = "";
    },
    convertToUppercase() {
      this.editingIata = this.editingIata.toUpperCase();
    },
  },
};
</script>

<style scoped>


</style>

