<template>
  <div>
    <h2>Login</h2>
    <p class="error" v-if="error !== ''"><span>Error:</span> {{ error }}</p>
    <form @submit.prevent="doLogin">
      <div>
        <input type="text" v-model="email" placeholder="Email Address" />
      </div>
      <div>
        <input type="password" v-model="password" placeholder="Password" />
      </div>
      <button type="submit">Login</button>
      <router-link to="/signup">Signup</router-link>
    </form>
  </div>
</template>

<script>
import { auth } from "../constants/firebase.js";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
      error: "",
    };
  },
  methods: {
    doLogin: function () {
      const { email, password } = this.$data;
      auth
        .signInWithEmailAndPassword(email, password)
        .then(() => {
          console.log("success");
        })
        .catch((err) => {
          console.error(err.code, err.message);
          this.error = err.message;
        });
    },
  },
};
</script>

<style>
.error span {
  font-weight: bold;
  color: red;
}
</style>
