<template>
    <div class="container contact-form">

        <div>
            <SideBar />
        </div>

        <form method="post">

            <div class="row">

                <div class="col-md-3"></div>

                <div class="col-md-6">

                    <h3>Drop Us a Question</h3>
                    <div class="form-group">
                        <input type="text" v-model="questionnaire.category" name="txtCategory" class="form-control"
                            placeholder="#hastag" value="person.category" />
                    </div>
                    <div class="form-group">
                        <textarea name="txtQuestion" v-model="questionnaire.question" class="form-control"
                            placeholder="Question " value="person.message"></textarea>
                    </div>
                    <div class="form-group">
                        <textarea name="txtQuestion" v-model="questionnaire.questionnaireDate" class="form-control"
                            placeholder="Question " value="person.message"></textarea>
                    </div>
                    <div class="form-group">
                        <input type="text" v-model="questionnaire.selectionOne" name="txtAge" class="form-control"
                            placeholder="selectionOne *" value="person.age" />
                    </div>
                    <div class="form-group">
                        <input type="text" v-model="questionnaire.selectionTwo" name="txtCoutry" class="form-control"
                            placeholder="selectionTwo *" value="person.country" />
                    </div>
                    <div class="form-group">
                        <input type="text" v-model="questionnaire.selectionThree" name="txtCity" class="form-control"
                            placeholder="selectionThree *" value="person.city" />
                    </div>
                    <div class="form-group">
                        <button type="button" @click="create()" class="btn btn-primary btn-lg">Create</button>
                    </div>

                </div>

            </div>
        </form>
    </div>
</template>
  
<script>
import router from "../router";
import SideBar from "../components/SideBar.vue"
import axios from "axios";
import jwt_decode from "jwt-decode";

export default {
    components: {
        SideBar,
    },

    data() {
        return {
            questionnaire: {
                selectionOne: "",
                selectionTwo: "",
                selectionThree: "",
                question: "",
                category: "",
                userId: ""
            },
        };
    },

    methods: {

        /**
         * kullanıcıdan aldığım verileri questionnasre tablosuna yazdırıyorum
         * @author Hakan Akbudak
         */
        create() {
            const token = localStorage.getItem("access_token"); 
            
            const decodedToken = jwt_decode(token);
            const userId = decodedToken._id;
            this.userId =userId
            console.log(token)
            console.log(decodedToken)

            axios
                .post(`http://localhost:3000/questionnaire/create/${userId}`, this.questionnaire, {
                    headers: {
                        "Authorization": `Bearer ${token}`, 
                        "Access-Control-Allow-Origin": "*", 
                        "Accept": "application/json",
                        "Content-Type": "application/json",
                    },
                    withCredentials: false,
                })
                .then(
                    (response) => {
                        console.log(response.data);
                        router.replace({
                            path: "/questionnaire",
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
  
<style>
.from-control textarea {
    width: 100%;
    height: 50px;
}
</style>