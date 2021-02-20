<template>
  <div id="app">
    <header>
      <div>
        <img src="./assets/logo.png" />
      </div>
      <div>
        <h1>Vote Tracker</h1>
      </div>
    </header>
    <router-view :userId="userId" :username="username" isAdmin="isAdmin" />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  max-width: 1080px;
  margin: 0 auto;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

header {
  max-width: 1080px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 2fr;
}
</style>

<script>
import firebase from "firebase";
import { firebaseConfig } from "./constants/firebase.js";
firebase.initializeApp(firebaseConfig);
export default {
  data() {
    return {
      userId: "",
      username: "",
      isAdmin: false,
    };
  },
  mounted() {
    firebase.auth().onAuthStateChanged((user) => {
      const { uid } = user;
      const dbRefUser = firebase.database().ref(`users/${uid}`);
      dbRefUser.once("value", (snapshot) => {
        const data = snapshot.val();
        this.userId = uid;
        this.username = data.username;
        this.isAdmin = data.isAdmin;
      });
    });
  },
};
</script>
