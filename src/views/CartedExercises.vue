<template>
<div class="saved">
  <br />
  <br />
  <br />
 
  <br />
  <!-- <h2>Hello {{ showName()}}!</h2> -->
  <br />
  <h2 class="text-uppercase"> Here is your saved workout list </h2>
  <p>Number of reps: 10-12</p>
  <p>Number of sets: 4</p>
  <br />
  


  <li class="list-group-item" v-for="carted in cartedExercises"> 
 <a :href="carted.exercise.description"> {{ carted.exercise.name }}</a></li>


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
h2 {
  font-size: 40px;
}
li {
  font-size: 20px;
}
</style>