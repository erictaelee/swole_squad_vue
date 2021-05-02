<template>
<div class="saved">
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <h2>Here is the list of workouts you've saved</h2>

  <h1> {{ cartedExercises }} </h1>

</div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      cartedExercises: [],
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
  },
};
</script>

