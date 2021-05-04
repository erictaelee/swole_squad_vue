<template>

  <div class="muscles">
               <!-- Masthead-->
        <header class="masthead">
            <div class="container">
                <!-- <div class="masthead-subheading">Welcome Swole Squad Fitness!</div> -->
                <br />
                <br />
                <br />
                
                <div class="masthead-heading text-uppercase">Train with Eric</div>
                <a class="btn btn-primary btn-xl text-uppercase js-scroll-trigger" href="#portfolio">Show Muscle Groups</a>
            </div>
        </header>

          <section class="page-section bg-light" id="portfolio">
            <div class="container">
                <div class="text-center">
                    <h2 class="section-heading text-uppercase">Muscle Groups</h2>
                    <h3 class="section-subheading text-muted">Click on the muscle group to see exercises.</h3>
                </div>
                <div class="row">
                    <div class="col-lg-4 col-sm-6 mb-4" v-for="muscle in muscles">
                        <div class="portfolio-item">
                            <a v-bind:href="`/muscles/${muscles.id}`" class="portfolio-link" data-toggle="modal" href="#portfolioModal1" v-on:click="exercisesShow(muscle)">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" v-bind:src="muscle.image_url" alt="..." />
                                
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">{{ muscle.name }}</div>
                                <!-- <div class="portfolio-caption-subheading text-muted">Illustration</div> -->
                            </div>
                        </div>
                    </div>

                </div>
            </div>
        </section>

        <!-- Portfolio Modals-->
        <!-- Modal 1-->
        <div class="portfolio-modal modal fade" id="portfolioModal1" tabindex="-1" role="dialog" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="container">
                        <div class="row justify-content-center">
                            <div class="col-lg-8">
                                <div class="modal-body">
                                    <!-- Project Details Go Here-->
                                    <h2 class="text-uppercase"> {{ selectedMuscle.name }}</h2>
                                    <!-- <p class="item-intro text-muted">Lorem ipsum dolor sit amet consectetur.</p> -->
                                 <p v-for="exercise in selectedMuscle.exercises"> <button v-on:click="exercisesCarted(exercise)">{{exercise.name}}</button> </p>   
                                                           
                                    <button class="btn btn-primary" data-dismiss="modal" type="button">
                                        <i class="fas fa-times mr-1"></i>
                                        Close Project
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    
    
    
    <!-- <div v-for="muscle in muscles">
      {{ muscle.name }}
      <p><button v-on:click="exercisesShow(muscle)"> Show Exercises </button></p>
      <img v-bind:src="muscle.image_url">
      <hr />
    </div>

    

    <dialog id="exercise-details">
      <form method="dialog">
      <h3>{{ selectedMuscle.name }} </h3>
      <br />
      <p v-for="exercise in selectedMuscle.exercises"> <button v-on:click="exercisesCarted(exercise)">{{exercise.name}}</button> </p>
      <button>Close</button>
      </form>
    </dialog> -->



<!-- <div v-for="carted in cartedExercises">
  
  <p>
   {{ carted.exercise.name }}: <a href=""> Click for the video </a></p>  </div> -->
  <!-- {{ cartedExercises[0].exercise.description }}   -->
      
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
      // document.querySelector("#exercise-details").showModal();
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


