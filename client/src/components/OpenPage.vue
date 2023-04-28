<template>
    <div class="open-page">
      <h1>OPEN PAGE</h1>
      <div>
        {{ result }}
        <PersonList/>
      </div>
    </div>
  </template>
  
  <script>
  import PersonList from '../components/PersonList.vue'
  import axios from "axios";
  export default {
    name: "OpenPage",
    data() {
      return {
        result: "",
      };
    },
    created() {
      this.getData();
    },
    methods: {
      getData() {
        axios
          .get("http://localhost:3000/getData", {
            headers: {
              "Access-Control-Allow-Origin": "*",
              Accept: "application/json",
              "Content-Type": "application/json",
              Authorization: localStorage.access_token,
            },
            withCredentials: false,
          })
          .then(
            (res) => {
              this.result = res.data;
              console.log("data get succesfully");
            },
            (error) => {
              console.log(error);
            }
          )
          .catch((e) => {
            console.log(e);
          });
      },
    },
    components:{
    PersonList,
  }
  };
  </script>