<template>
  <div>
    <h2>Add a New Airport</h2>
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
  </div>
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

        // check if iata is empty
        if (this.iata === "") {
          this.iataError = "IATA code is required.";
          isValid = false;
          // check if matches 3 uppercase letters
        } else if (!this.iata.match(/^[A-Z]{3}$/)) {
         
          this.iataError = "IATA code must be 3 uppercase letters.";
          isValid = false;
        }

        // check if name is empty
        if (this.name === "") {
          this.nameError = "Airport name is required.";
          isValid = false;
        }

        return isValid; 
      },

      handleSubmit() {
        // if validate returns true
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
  
  h2 {
    margin-bottom: 1em;
  }

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
    margin-top: 5px;
    cursor: pointer; 
  }

  .button-submit:hover {
    background-color: #279119; 
  }

</style>
  
  
  
  