<template>
  <div class="muscles">
    <h1>{{ message }}</h1>
    
    
    <div v-for="muscle in muscles">
      {{ muscle.name }}
      <p><button v-on:click="exercisesShow(muscle)"> Show Exercises </button></p>
      <img v-bind:src="muscle.image_url">
      <hr />
    </div>


<!-- <div v-for="carted in cartedExercises"> -->
  {{ cartedExercises }} 
  <!-- <p>
  <a href=""> {{ carted.exercise }}</a></p>  </div> -->
  <!-- {{ cartedExercises[0].exercise.description }}   -->


    <dialog id="exercise-details">
      <form method="dialog">
      <h2>Here will be some list of exercises</h2>
      <p>name: {{ selectedMuscle.name }} </p>
      <p v-for="exercise in selectedMuscle.exercises"> <button v-on:click="exercisesCarted(exercise)">{{exercise.name}}</button>: {{ exercise.description }} </p>
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
      selectedMuscle: {},
      exercise: {},
      cartedExercises: [],
    };
  },
  created: function () {
    this.musclesIndex();
    this.cartedIndex();
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
      this.selectedMuscle = theExercise;
      document.querySelector("#exercise-details").showModal();
      // axios.get("http://localhost:3000/api/exercises").then((response) => {
      //   console.log(response.data);
      //   this.exercises = response.data;
      // });
    },
    exercisesCarted: function (exercisesCarted) {
      console.log(exercisesCarted);
      console.log(this.selectedMuscle);
      console.log("carted...");
      var params = {
        muscle_id: this.selectedMuscle.id,
        exercise_id: exercisesCarted.id,
      };
      axios
        .post("http://localhost:3000/api/carted_exercises", params)
        .then((response) => {
          console.log(response.data);
          this.carted_exercises = response.data;
        });
    },
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