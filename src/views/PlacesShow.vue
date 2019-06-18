<template>
  <div class="places-show">
    <h1>{{ place.name }}</h1>
    <br>
    <h3>{{ place.address }}</h3>
    <button>
      <router-link :to="'/places/' + place.id + '/edit'">Edit Place</router-link>
    </button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      place: ""

    };
  },
  created: function() {
    axios.get("/api/places/" + this.$route.params.id).then(response => {
      this.place = response.data;
      console.log(this.place);
    })
  },
  methods: {}
};
</script>