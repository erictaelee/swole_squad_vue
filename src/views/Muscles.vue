<template>

  <div class="muscles">
               <!-- Masthead-->
        <header class="masthead">
            <div class="container">
                <div class="masthead-subheading">Welcome Swole Squad Fitness!</div>
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
                    <div class="col-lg-4 col-sm-6 mb-4">
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-toggle="modal" href="#portfolioModal1">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/muscle_images/Abs.jpeg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">Threads</div>
                                <div class="portfolio-caption-subheading text-muted">Illustration</div>
                            </div>
                        </div>
                    </div>
                    <!-- <div class="col-lg-4 col-sm-6 mb-4">
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-toggle="modal" href="#portfolioModal2">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/02-thumbnail.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">Explore</div>
                                <div class="portfolio-caption-subheading text-muted">Graphic Design</div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-4 col-sm-6 mb-4">
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-toggle="modal" href="#portfolioModal3">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/03-thumbnail.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">Finish</div>
                                <div class="portfolio-caption-subheading text-muted">Identity</div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-4 col-sm-6 mb-4 mb-lg-0">
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-toggle="modal" href="#portfolioModal4">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/04-thumbnail.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">Lines</div>
                                <div class="portfolio-caption-subheading text-muted">Branding</div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-4 col-sm-6 mb-4 mb-sm-0">
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-toggle="modal" href="#portfolioModal5">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/05-thumbnail.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">Southwest</div>
                                <div class="portfolio-caption-subheading text-muted">Website Design</div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-4 col-sm-6">
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-toggle="modal" href="#portfolioModal6">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/06-thumbnail.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">Window</div>
                                <div class="portfolio-caption-subheading text-muted">Photography</div>
                            </div>
                        </div>
                    </div> -->
                </div>
            </div>
        </section>

    <h1>{{ message }}</h1>
    
    
    <div v-for="muscle in muscles">
      {{ muscle.name }}
      <p><button v-on:click="exercisesShow(muscle)"> Show Exercises </button></p>
      <img v-bind:src="muscle.image_url">
      <hr />
    </div>

    


<div v-for="carted in cartedExercises">
  
  <p>
   {{ carted.exercise.name }}: <a href=""> Click for the video </a></p>  </div>
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