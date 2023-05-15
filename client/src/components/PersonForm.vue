<template>
  <div class="container contact-form">
    <div class="contact-image">
      <img src="https://image.ibb.co/kUagtU/rocket_contact.png" alt="rocket_contact" />
    </div>
    <form method="post">
      <h3>Drop Us a Message</h3>
      <div class="row">
        <div class="col-md-6">

          <div class="form-group">
            <input list="category" v-model="person.category" placeholder="selected">
            <datalist id="category">
              <option value="#araba" href="http://localhost:8080/"><a href="http://localhost:8080/"></a></option>
              <option value="Bentley"></option>
              <option value="Mercedes"></option>
              <option value="Audi"></option>
              <option value="Volkswagen"></option>
            </datalist>
          </div>

          <div class="form-group">
            <input type="text" v-model="person.age" name="txtName" class="form-control" placeholder="Your Age *"
              value="person.age" />
          </div>
          <div class="form-group">
            <input type="text" v-model="person.country" name="txtEmail" class="form-control" placeholder="Your Country *"
              value="person.country" />
          </div>
          <div class="form-group">
            <input type="text" v-model="person.city" name="txtPhone" class="form-control" placeholder="Your City *"
              value="person.city" />
          </div>
          <div class="form-group">
            <button type="button" @click="create" class="btn btn-primary btn-lg"
              style="padding-left: 2.5rem; padding-right: 2.5rem;">Create</button>
          </div>
        </div>
        <div class="col-md-6">
          <div class="form-group">
            <textarea name="txtMsg" v-model="person.message" class="form-control" placeholder="Your Message *"
              style="width: 100%; height: 150px;" value="person.message"></textarea>
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
        age: "",
        country: "",
        city: "",
        message: "",
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
  },

};
</script>

<style></style>