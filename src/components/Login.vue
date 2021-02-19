<template>
  <div>
    <h2>Login</h2>
    <form>
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
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
};
</script>
