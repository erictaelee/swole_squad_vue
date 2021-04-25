<template>
  <div class="muscles">
    <h1>{{ message }}</h1>
    
    <button v-on:click="exercisesShow">Show Exercises </button>
    <div v-for="muscle in muscles">
      {{ muscle.name }}
      <img v-bind:src="muscle.image_url">
      <hr />
    </div>
    
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Click on the muscle group!",
      muscles: [],
    };
  },
  created: function () {
    this.musclesIndex();
  },
  methods: {
    musclesIndex: function () {
      console.log("in muscles index");
      axios.get("http://localhost:3000/api/muscles").then((response) => {
        console.log(response.data);
        this.muscles = response.data;
      });
    },
    exercisesShow: function () {
      console.log("in exercises show");
    },
  },
};
</script>