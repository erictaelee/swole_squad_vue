<template>
  <div class="muscles">
    <h1>{{ message }}</h1>
    
    
    <div v-for="muscle in muscles">
      {{ muscle.name }}
      <p><button v-on:click="exercisesShow(exercise)"> Show Exercises </button></p>
      <img v-bind:src="muscle.image_url">
      <hr />
    </div>

    <dialog id="exercise-details">
      <form method="dialog">
      <h2>Here will be some list of exercises</h2>
      <p>name: {{ selectedExercise.name }} </p>
      <button>Close</button>
      </form>
    </dialog>
    
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
      selectedExercise: {},
      exercise: {},
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
    exercisesShow: function (theExercise) {
      console.log("in exercises show");
      console.log(theExercise);
      this.selectedExercise = theExercise;
      document.querySelector("#exercise-details").showModal();
      axios.get("http://localhost:3000/api/exercises").then((response) => {
        console.log(response.data);
        this.exercises = response.data;
      });
    },
  },
};
</script>