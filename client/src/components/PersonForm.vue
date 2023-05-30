<template>
  <div class="container contact-form">

    <form method="post">

      <div class="row">

        <div class="col-md-3"></div>

        <div class="col-md-6">

          <h3>Drop Us a Question</h3>

          <div class="form-group">
            <input type="text" v-model="person.category" name="txtCategory" class="form-control" placeholder="#hastag"
              value="person.category" />
          </div>

          <div class="form-group">
            <textarea name="txtQuestion" v-model="person.question" class="form-control" placeholder="Question "
              style="width: 100%; height: 50px;" value="person.message"></textarea>
          </div>
          <div class="form-group">
            <input type="text" v-model="person.selectionOne" name="txtAge" class="form-control"
              placeholder="selectionOne *" value="person.age" />
          </div>
          <div class="form-group">
            <input type="text" v-model="person.selectionTwo" name="txtCoutry" class="form-control"
              placeholder="selectionTwo *" value="person.country" />
          </div>
          <div class="form-group">
            <input type="text" v-model="person.selectionThree" name="txtCity" class="form-control"
              placeholder="selectionThree *" value="person.city" />
          </div>
          <div class="form-group">
            <button type="button" @click="create()" class="btn btn-primary btn-lg"
              style="padding-left: 2.5rem; padding-right: 2.5rem;">Create</button>

            <button type="button" @click="updateQuestionnaire()" class="btn btn-primary btn-lg"
              style="padding-left: 2.5rem; padding-right: 2.5rem; background-color: green;">Update</button>

          </div>

        </div>

      </div>
    </form>
  </div>
</template>

<script>
import router from "../router";
import axios from "axios";
export default {

  data() {
    return {
      person: {
        selectionOne: "",
        selectionTwo: "",
        selectionThree: "",
        question: "",
        category: "",
      },
    };
  },

  methods: {

    create() {
      axios
        .post("http://localhost:3000/questionnaire", this.person, {
          headers: {
            "Access-Control-Allow-Origin": "http://localhost:3000/questionnaire",
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          withCredentials: false,
        })
        .then(
          (response) => {
            console.log(response.data);
            localStorage.access_token = response.data;
            router.replace({
              path: "/openpage",
            });
          },
          (error) => {
            console.log(error);
          }
        );
    },


    //put isteği
    async updateQuestionnaire(_id) {
      try {
        const { id } = this.$route.params;
        const { selectionOne, selectionTwo, selectionThree, question, category } = this.person;


        const response = await axios.put(`http://localhost:3000/questionnaire/${id}`, {
          selectionOne,
          selectionTwo,
          selectionThree,
          question,
          category
        });

        const updatedPerson = response.data;

        router.replace({
          path: "/openpage",
        });
        console.log(updatedPerson);
      } catch (error) {
        console.log(error)
      }
    },

  },

};
</script>

<style></style>