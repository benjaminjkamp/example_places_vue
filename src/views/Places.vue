<template>
  <div class="places">
    <h1>{{ message }}</h1><br><br>
    <div v-for="place in places">
      <h2> <router-link :to="'/places/' + place.id"> {{ place.name }}: {{ place.address}} </router-link></h2><br>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Example Places!",
      places: []
    };
  },
  created: function() {
    axios.get("/api/places").then(response =>{
      this.places = response.data;
      console.log(this.places);
    });
  },
  methods: {}
};
</script>