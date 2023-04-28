<template>
  <div class="home">
    <br>
    <button type="button" @click="goToLogin" class="btn btn-primary btn-lg"
      style="padding-left: 2.5rem; padding-right: 2.5rem;">Login</button>
      <br><br>

    <button type="button"  @click="goToRegister" class="btn btn-primary btn-lg"
      style="padding-left: 2.5rem; padding-right: 2.5rem;">Register</button>

  </div>
</template>

<script>

import router from "../router";
export default {
  name: "LoginPage",
  methods: {
    goToRegister() {
      router.replace({
        path: "/register",
      });
    },
    goToLogin() {
      router.replace({
        path: "/login",
      });
    },
  },

};
</script>