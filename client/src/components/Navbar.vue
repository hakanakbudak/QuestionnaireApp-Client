<template>
  <div>

    <nav class="navbar">

      <div>

        <button class="navBtn" type="button" @click="homeBtn()">Home</button>
        <button class="navBtn" type="button" @click="loginBtn()">Login</button>

      </div>
    </nav>

  </div>
</template>

<script>

import router from "../router";
import axios from "axios";

export default {

  methods: {

    homeBtn() {
      router.replace({
        path: "/",
      });
    },

    loginBtn() {
      router.replace({
        path: "/login",
      });
    },
  }
}
</script>

<style>
nav {
  /*background-color: chocolate;
  background: linear-gradient(90deg, rgba(2, 0, 36, 1) 0%, rgba(9, 9, 121, 1) 35%, rgba(0, 212, 255, 1) 100%);*/
  background: linear-gradient(90deg, rgb(2, 9, 121, 1) 20%, rgb(11, 134, 235) 45%, rgb(0, 9, 121, 1) 100%);
  height: 60px;

}

.navBtn {
  color: white;
  outline: 0;
  border: 2px solid currentcolor;
  border-color: darkblue;
  transition: 0.3s ease all;
  background-color: rgba(220, 220, 220, 0.556);
  font-size: 15px;
  font-weight: 600;
  padding: 10px 25px;
  display: inline-block;
  position: relative;
  left: 1300px;

}

.navBtn:hover {
  color: white;
  border-color: transparent;
  background-color: dodgerblue;
  border-radius: 8px;

}
</style>