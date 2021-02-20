<template>
  <div class="home">
    <Login v-if="userId === ''" />
    <VoteAdmin v-else-if="userId !== '' && isAdmin" />
    <Voter v-else />
  </div>
</template>

<script>
// @ is an alias to /src
import Login from "@/components/Login.vue";
import VoteAdmin from "@/components/VoteAdmin.vue";
import Voter from "@/components/Voter.vue";

export default {
  name: "Home",
  props: {
    userId: String,
    username: String,
    isAdmin: Boolean,
  },
  components: {
    Login,
    VoteAdmin,
    Voter,
  },
};
</script>
