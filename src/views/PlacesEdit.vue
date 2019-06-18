<template>
  <div class="home">
    <h1>Edit Place</h1>

    Name: <input type="text" v-model="place.name"><br>
    Address: <input type="text" v-model="place.address"><br>
    <ul>
      <li v-for="error in errors">{{errors}}</li>
    </ul>
    <button v-on:click="submit()">Edit Place</button>
    <br>
    <button v-on:click="destroy()">Delete Place</button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      place: "",
      errors: []
    };
  },
  created: function() {
    axios.get("/api/places/" + this.$route.params.id).then(response => {
      console.log(response.data);
      this.place = response.data;
      
    })
  },
  methods: {
    submit: function() {
      var params = {
        name: this.place.name,
        address: this.place.address
      };
      axios.patch("/api/places/" + this.place.id, params).then(response => {
        console.log("Updated", response.data);
        this.place = response.data;
        this.$router.push("/places/" + this.place.id);
      }).catch(error => {
        console.log(error.response.data);
        this.errors = error.response.data;
        
      })
    },
    destroy: function() {
      axios.delete("/api/places/" + this.$route.params.id).then(response => {
        console.log("deleted", response.data);
        this.$router.push("/places");
      })
    }
  }
};
</script>