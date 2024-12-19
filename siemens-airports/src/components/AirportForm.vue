<template>
    <form v-on:submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="iata">IATA Code:</label>
        <input
          id="iata"
          type="text"
          v-model="iata"
          maxlength="3"
          v-on:input="convertToUppercase"
        />
        <span v-if="iataError" class="error">{{ iataError }}</span>
      </div>
      <div class = "form-group">
        <label for="name">Airport Name:</label>
        <input id="name" type="text" v-model="name"/>
        <span v-if="nameError" class="error">{{ nameError }}</span>
      </div>
      <button type="submit" class="button-submit">Add Airport</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        iata: "",
        name: "",
        iataError: "",
        nameError: "",
      };
    },
    methods: {
      convertToUppercase() {
        this.iata = this.iata.toUpperCase();
      },
      validate() {
        this.iataError = "";
        this.nameError = "";
        
        let isValid = true;

        // Check if IATA is empty
        if (this.iata === "") {
          this.iataError = "IATA code is required.";
          isValid = false;
        } else if (!this.iata.match(/^[A-Z]{3}$/)) {
          // Check if IATA matches the pattern
          this.iataError = "IATA code must be 3 uppercase letters.";
          isValid = false;
        }

        // Check if name is empty
        if (this.name === "") {
          this.nameError = "Airport name is required.";
          isValid = false;
        }

        return isValid; // Only return true if all validations pass
      },

      handleSubmit() {
        if (this.validate()) {
          this.$emit("add-airport", { iata: this.iata, name: this.name });
          this.iata = "";
          this.name = "";
        }
      },
    },
  };
  </script>
  
  <style scoped>
  
  .form-group {
    display: flex;
    align-items: center; 
    margin-bottom: 1em; 
  }
  
  label {
    width:7em; 
    font-weight: bold; 
  }
  
  input {
    padding: 0.3em; 
    margin-right: 0.8em; 
  }
  
  .error {
    color: red;
    font-size: 1em; 
  }

  .button-submit {
    background-color: #27911998; 
    color: rgb(255, 255, 255); 
    padding: 10px; 
    font-size: 16px; 
    font-weight: bold; 
    border: none; 
    border-radius: 3px; 
    cursor: pointer; 
  }

  .button-submit:hover {
    background-color: #279119; 
  }
  </style>
  
  
  
  