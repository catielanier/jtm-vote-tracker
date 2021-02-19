<template>
  <div>
    <h2>Signup</h2>
    <form @submit.prevent="doSignup">
      <div>
        <input type="text" v-model="email" placeholder="Email Address" />
      </div>
      <div>
        <input type="password" v-model="password" placeholder="Password" />
      </div>
      <div>
        <input type="password" v-model="verifyPassword" placeholder="Verify Password" />
      </div>
      <div>
        <input type="text" v-model="username" password="Username" />
      </div>
      <button type="submit">Signup</button>
      <router-link to="/">Login</router-link>
    </form>
  </div>
</template>

<script>
import firebase from "firebase";
export default {
  name: "Signup",
  data() {
    return {
      email: "",
      password: "",
      verifyPassword: "",
      username: "",
    };
  },
  methods: {
    doSignup: function () {
      const { email, password, verifyPassword, username } = this.$data;
      if (password === verifyPassword) {
        firebase
          .auth()
          .createUserWithEmailAndPassword(email, password)
          .then((res) => {
            const dbRef = firebase.database().ref(`users/${res.user.uid}`);
            dbRef.set({ username, email });
          })
          .catch((err) => console.error(err.code, err.message));
      } else {
        console.error("Passwords don't match.");
      }
    },
  },
};
</script>
