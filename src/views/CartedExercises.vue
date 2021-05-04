<template>
<div class="saved">
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  {{ showName()}}
  <h2>Here is your saved workouts</h2>
  <br />

  <div v-for="carted in cartedExercises"> 
 <a :href="carted.exercise.description"> {{ carted.exercise.name }}</a></div>


</div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      cartedExercises: [],
      name: "",
    };
  },

  created: function () {
    this.cartedIndex();
  },
  methods: {
    cartedIndex: function () {
      console.log("hello");
      axios
        .get("http://localhost:3000/api/carted_exercises")
        .then((response) => {
          console.log(response.data);
          this.cartedExercises = response.data;
        });
    },
    showName: function () {
      return localStorage.getItem("name");
    },
  },
};
</script>

<style>
</style>