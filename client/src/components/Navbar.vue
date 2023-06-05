<template>
  <div>
    <nav class="navbar">
      
      <div>
        <button class="nav-bar-button" type="button" @click="loginViewButton()">Login</button>
      </div>
    </nav>
  </div>
</template>

<script>

import router from "../router";
import axios from "axios";

export default {

  methods: {

    loginViewButton() {
      router.replace({
        path: "/login",
      });
    },
  }
}
</script>

<style>
nav {
  background: linear-gradient(90deg, rgb(2, 9, 121, 1) 20%, rgb(11, 134, 235) 45%, rgb(0, 9, 121, 1) 100%);
  height: 60px;

}

.nav-bar-button {
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
  left: 1400px;

}

.nav-bar-button:hover {
  color: white;
  border-color: transparent;
  background-color: dodgerblue;
  border-radius: 8px;
}

.title-text{
  margin-left: 100px;
}
</style>