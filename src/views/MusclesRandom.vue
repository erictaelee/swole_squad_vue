<template>
  <div class="muscles-random">
    <h1>{{ message }}</h1>
    <button v-on:click="getRandomMuscleFrontend">Get Random Muscle (frontend) </button>
    <p>{{ randomMuscle }}</p>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the random page",
      randomMuscle: {},
    };
  },
  created: function () {},
  methods: {
    getRandomMuscleFrontend: function () {
      console.log("getting muscle...");
      axios.get("/api/muscles").then((response) => {
        console.log(response.data);
        this.randomMuscle =
          response.data[Math.floor(Math.random() * response.data.length)];
        console.log(this.randomMuscle);
      });
    },
  },
};
</script>