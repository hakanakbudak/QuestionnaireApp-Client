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

            <button type="button" @click="updatePerson()" class="btn btn-primary btn-lg"
              style="padding-left: 2.5rem; padding-right: 2.5rem;">Create</button>

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
        const { selectionOne, selectionTwo, selectionThree, question, category } = this.person
        const response = axios.put(`http://localhost:3000/update/${_id, selectionOne, selectionTwo, selectionThree, question,category}`)

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

<style></style>