<template>
  <div>

    <h6>{{ result }}</h6><br>
    <div>
      <PersonList />
    </div>

  </div>
</template>

  
<script>
import PersonList from '../components/PersonList.vue'
import axios from "axios";


export default {
  components: {
    PersonList,
  },

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
            "Access-Control-Allow-Origin": "http://localhost:3000/getData",
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

};
</script>