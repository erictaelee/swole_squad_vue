<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h3> Please login to continue </h3>
 
    </div>
    
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Swole Squad Fitness App!",
    };
  },
  created: function () {},
  methods: {},
};
</script>