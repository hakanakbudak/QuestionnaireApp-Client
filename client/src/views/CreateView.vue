<template>

  <div>
    <div>
      <SideBar/>
    </div>

    <div>
      <PersonForm/>
    </div>
    
  </div>
</template>

<script>
import SideBar from "../components/SideBar.vue"
import PersonForm from "../components/PersonForm.vue"
import router from "../router";
import axios from "axios";

export default {
  components: {
    SideBar,
    PersonForm,
  },

  data() {
    return {
      person: {
        age: "",
        country: "",
        city: "",
        message: "",
      },
    };
  },
  methods: {
    create() {
      axios
        .post("http://localhost:3000/create", this.person, {

        })
        .then(
          (response) => {
            console.log(response);
            router.replace({
              path: "/openpage",
            });
          },
          (error) => {
            console.log(error);
          }
        );
    },
  },

};
</script>