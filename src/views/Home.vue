<template>

  <div class="login">
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <form v-on:submit.prevent="submit()">
      <h1>Swole Squad</h1>
      <p>Please sign in to continue</p>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email">
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
    <br />
  <p>Don't have an account? </p>
  <router-link to="/signup">Sign up</router-link>
  </div>

</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      email: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/api/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          this.$router.push("/team");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>

<style>
.form-group {
  padding-right: 300px;
  padding-left: 300px;
}
</style>