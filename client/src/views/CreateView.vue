<template>
  <div>
    <div>
      <SideBar />
    </div>

    <div>
      <PersonForm />
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
        selectionOne: "",
        selectionTwo: "",
        selectionThree: "",
        question: "",
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

    updatePerson(_id) {
      try {
        const { selectionOne, selectionTwo, selectionThree, question } = this.person
        const response = axios.put(`http://localhost:3000/create/${_id, selectionOne, selectionTwo, selectionThree, question}`)

        response.then((res) => {
          this.person = res.data // response'dan gelen veriyi person veri modeline atayın
        })
      } catch (error) {
        console.log(error)
      }
    },


  },

};
</script>