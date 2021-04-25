<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="muscle in muscles">
      {{ muscle.name }}
      <hr />
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
  },
};
</script>