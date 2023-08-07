<template>
  <div>
    <nav class="navbar">
      
      <div>
        <button class="nav-bar-button" type="button" @click="loginViewButton()">Login</button><span>.</span>
        <button class="nav-bar-button" type="button" @click="registerViewButton()">Register</button>
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

    registerViewButton(){
      router.replace({
        path: "/register",
      });
    }
  }
}
</script>

<style>
nav {
  background-color: transparent;
  height: 60px;
}
.nav-bar-button {
  color: white;
  outline: 0;
  border: 2px solid currentcolor;
  border-color: darkblue;
  transition: 0.3s ease all;
  background-color: transparent;
  font-size: 15px;
  font-weight: 600;
  padding: 10px 25px;
  display: inline-block;
  position: relative;
  left: 1250px;
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