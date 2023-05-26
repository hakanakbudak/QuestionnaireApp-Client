<template>

  
  <div>
    <div>
      <NavBar/>
    </div>
    <div class="row">
      <div class="col-sm-3"></div>

      <div class="col-sm-5"><br>

        
        <br>

        <div v-for="person in persons" :key="person._id" class="card my-4">

          <div class="card">
            <div class="card-body">

              <ul class="list-group list-group-vertical">
                <h5 class="card-title">{{ person.category }}</h5>
                <li class="list-group-item">{{ person.selectionOne }}</li>
                <li class="list-group-item">{{ person.selectionTwo }}</li>
                <li class="list-group-item">{{ person.selectionThree }} </li>
                <li class="list-group-item">{{ person.question }} </li>
              </ul>

            </div>

          </div>

        </div>

      </div>
      <div class="col-sm-3"></div>

    </div>
  </div>
</template>

<script>

//import HomePage from "@/components/HomePage.vue";

import router from "../router";
import axios from "axios";
import NavBar from "../components/NavBar.vue"

export default {
  name: "LoginPage",

  components: {
    NavBar,
  },

  data() {
    return {
      persons: []
    }
  },

  created() {
    this.getPersons()
  },


  methods: {
    async getPersons() {
      try {
        const response = await axios.get('http://localhost:3000/persons')
        this.persons = response.data


      } catch (error) {
        console.error(error)
      }
    },
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

<style>
.search-bar {
  width: auto;
  height: auto;
  border-radius: 10px;
  border-color: black;
  text-align: center;
  margin-left: 10px;
  margin-top: 10px;
}

.search-area {
  margin-bottom: 0;
  width: 615px;
  height: 50px;
  background-color: rgba(0, 0, 139, 0.137);
  z-index: 1;
  border-radius: 10px;
}
</style>