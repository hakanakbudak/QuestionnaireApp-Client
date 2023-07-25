<template>
  <div class="container contact-form">
    <div>
      <SideBar />
    </div>
    <form method="post">
      <div class="row">
        <div class="col-md-3"></div>
        <div class="col-md-6">
          <table>
            <h3 class="form-title">Drop Us a Question</h3>
            <tr>
              <div class="form-group">
                <input type="text" v-model="questionnaire.category" name="txtCategory" class="form-control"
                  placeholder="#hastag" value="questionnaire.category" />
              </div>
            </tr>
            <tr>
              <div class="form-group">
                <textarea name="txtQuestion" v-model="questionnaire.question" class="form-control" placeholder="Question "
                  value="questionnaire.question"></textarea>
              </div>
            </tr>
            <tr>
              <div class="form-group">
                <input type="text" v-model="questionnaire.selectionOne" name="txtAge" class="form-control"
                  placeholder="selectionOne *" value="questionnaire.selectionOne" />
              </div>
            </tr>
            <tr>
              <div class="form-group">
                <input type="text" v-model="questionnaire.selectionTwo" name="txtCoutry" class="form-control"
                  placeholder="selectionTwo *" value="questionnaire.selectionTwo" />
              </div>
            </tr>
            <tr>
              <div class="form-group">
                <input type="text" v-model="questionnaire.selectionThree" name="txtCity" class="form-control"
                  placeholder="selectionThree *" value="questionnaire.selectionThree" />
              </div>
            </tr>
            <tr>
              <div class="form-group">
                <button type="button" @click="updateQuestionnaire()" class="btn btn-primary btn-lg">Update</button>
              </div>
            </tr>
          </table>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import router from "../router";
import axios from "axios";
import SideBar from "../components/SideBar.vue"
export default {
  components: {
    SideBar,
  },
  data() {
    return {
      questionnaire: {
        selectionOne: null,
        selectionTwo: null,
        selectionThree: null,
        question: null,
        category: null,
      },
    };
  },
  methods: {
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
        //const updatedQuestionnaire = response.data;
        router.replace({
          path: "/questionnaire",
        });
        this.questionnaire=response.data
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
.form-control{
  width: 500px;
}
.btn{
  width: 500px;
}
.form-title {
    font-size: 60px;
    font-style: oblique;
    
}
.button {
  padding-left: 2.5rem;
  padding-right: 2.5rem;
  background-color: green;
}
</style>