<template>
  <div class="container contact-form">

    <form method="post">

      <div class="row">

        <div class="col-md-3"></div>

        <div class="col-md-6">

          <h3>Drop Us a Question</h3>
          <div class="form-group">
            <input type="text" v-model="questionnaire.category" name="txtCategory" class="form-control"
              placeholder="#hastag" value="questionnaire.category" />
          </div>
          <div class="form-group">
            <textarea name="txtQuestion" v-model="questionnaire.question" class="form-control" placeholder="Question "
              value="questionnaire.question"></textarea>
          </div>
          <div class="form-group">
            <input type="text" v-model="questionnaire.selectionOne" name="txtAge" class="form-control"
              placeholder="selectionOne *" value="questionnaire.selectionOne" />
          </div>
          <div class="form-group">
            <input type="text" v-model="questionnaire.selectionTwo" name="txtCoutry" class="form-control"
              placeholder="selectionTwo *" value="questionnaire.selectionTwo" />
          </div>
          <div class="form-group">
            <input type="text" v-model="questionnaire.selectionThree" name="txtCity" class="form-control"
              placeholder="selectionThree *" value="questionnaire.selectionThree" />
          </div>
          <div class="form-group">
            <button type="button" @click="create()" class="btn btn-primary btn-lg"
              >Create</button>
            <button type="button" @click="updateQuestionnaire()" class="btn btn-primary btn-lg"
              >Update</button>
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
      questionnaire: {
        selectionOne: "",
        selectionTwo: "",
        selectionThree: "",
        question: "",
        category: "",
      },
    };
  },

  methods: {

    /**
     * kullanıcıdan aldığım verileri questionnaire tablosuna yazdırma işlemi yapıyorum. 
     */
    create() {
      axios
        .post("http://localhost:3000/questionnaire", this.questionnaire, {
          headers: {
            "Access-Control-Allow-Origin": "*",
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


    /**
     * questionnaire tablosu içerisinde bulunan anket veirlerini id üzerinden update işlemi gerçekleştiriyorum. 
     * @author Hakan Akbudak
     */
    async updateQuestionnaire(_id) {
      try {
        const { id } = this.$route.params;
        const { selectionOne, selectionTwo, selectionThree, question, category } = this.questionnaire;


        const response = await axios.put(`http://localhost:3000/questionnaire/${id}`, {
          selectionOne,
          selectionTwo,
          selectionThree,
          question,
          category
        });

        const updatedQuestionnaire = response.data;

        router.replace({
          path: "/openpage",
        });
        console.log(updatedQuestionnaire);
      } catch (error) {
        console.log(error)
      }
    },

  },

};
</script>

<style>
.from-control textarea {
  width: 100%;
  height: 50px;
}

.button{
  padding-left: 2.5rem; 
  padding-right: 2.5rem; 
  background-color: green;
}
</style>