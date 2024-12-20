<template>
  <div>
    <h2>Airport List</h2>
    <ul>
      <li v-for="(airport, index) in airports" :key="index" class="airport-item">
        <div v-if="editingIndex === index">
          <input
            class = "edit-input"
            v-model="editingIata"
            maxlength="3"
            placeholder="IATA Code"
            v-on:input="convertToUppercase"
          />
          <input class = "edit-input" v-model="editingName" placeholder="Airport Name"/>
          <button class="btn save" v-on:click="saveEdit(index)">Save</button>
          <button class="btn cancel" v-on:click="cancelEdit">Cancel</button>
        </div>
        <div v-else>
          <span class="airport-text">{{ airport.iata }} | {{ airport.name }}</span>
          <button class="btn edit" v-on:click="editAirport(index, airport)">Edit</button>
          <button class="btn delete" v-on:click="deleteAirport(index)">Delete</button>
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
      // check again data validation
      if (!this.editingIata.match(/^[A-Z]{3}$/)) {
        alert("IATA code must be 3 uppercase letters.");
        return;
      }
      if (this.editingName === "") {
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

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.edit-input {
  padding: 5px;
  margin-right: 10px;
}

ul {
  padding: 0;
}

.airport-item {
  padding: 10px;
  margin-bottom: 5px;
  border: 2px solid #ff590c7a;
}

.airport-text {
  font-size: 15px;
  font-weight: bold; 
}

.btn {
  padding: 5px 10px;
  margin-left: 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}

.btn.save {
  background-color: #1b771eb2;
  color: white;
}

.btn.cancel {
  background-color: #f44336d0;
  color: white;
}

.btn.edit {
  background-color: #2195f3bb;
  color: white;
}

.btn.delete {
  background-color: #ff2222c5;
  color: white;
}

.btn.save:hover {
  background-color: #1b771e;
}

.btn.cancel:hover {
  background-color: #f44336;
}

.btn.edit:hover {
  background-color: #2195f3;
}

.btn.delete:hover {
  background-color: #ff2222;
}
</style>
