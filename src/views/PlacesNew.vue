<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <br><br>
    Name: <input type="text" v-model="newPlaceName"><br>
    Address: <input type="text" v-model="newPlaceAddress"><br>
    <ul>
      <li v-for="error in errors">{{ errors }}</li>
    </ul>
    <button type="submit" v-on:click="submit()">Add Place</button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "New Place!",
      newPlaceName: "",
      newPlaceAddress: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    submit: function(){
      var params = {
        name: this.newPlaceName,
        address: this.newPlaceAddress
      };

      axios.post("/api/places", params).then(response => {
        console.log("Success", response.data);
        this.$router.push("/places");

      }).catch(error => {
        this.errors = error.response.data;
        console.log(error.response.data);
      })
    }
  }
};
</script>