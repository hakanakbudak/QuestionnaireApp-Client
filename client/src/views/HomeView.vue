<template>
  <div>
    <NavBar />
    <div class="row">

      <div class="col-sm-3">

      </div>

      <div class="col-sm-5">
        <br>
        <div v-for="questionnaire in questionnaires" :key="questionnaire._id" class="card my-4">

          <div class="card">
            <div class="card-body">

              <ul class="list-group list-group-vertical">

                <li class="list-group-item">
                  <h2 class="card-title">{{ questionnaire.category }}</h2>
                </li>

                <li class="list-group-item">
                  <h5>{{ questionnaire.question }}</h5>
                  <p class="date-text">{{ currentDate }},{{ currentTime }}</p>
                </li>

                <li class="list-group-item">{{ questionnaire.selectionOne }} <br>
                </li>

                <li class="list-group-item">{{ questionnaire.selectionTwo }} <br>
                </li>

                <li class="list-group-item">{{ questionnaire.selectionThree }} <br>
                </li>
              </ul>
              <br>
            </div>
            
          </div>

        </div>
      </div>

      <div class="col-sm-3">
      </div>

    </div>

  </div>
</template>

<script>

import router from "../router";
import axios from "axios";
import NavBar from "../components/NavBar.vue"

export default {

  components: {
    NavBar,
  },

  data() {
    return {
      questionnaires: [],

    }
  },

  created(){
    this.getPersons()
  },

  methods: {

    /**
     * questionnaire tablosundan verileri get metodu ile çağırıyorum.
     * @author Hakan Akbudak
     */
    async getPersons() {
            try {
                const response = await axios.get('http://localhost:3000/questionnaire',)
                this.questionnaires = response.data
            } catch (error) {
                console.error(error)
            }
        },

        /*
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
    */
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