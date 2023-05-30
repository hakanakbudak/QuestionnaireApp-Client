<template>
    <div>
        <SideBar />
        <div class="row">

            <div class="col-sm-3">

            </div>

            <div class="col-sm-5">

                <div class="search-area">
                    <input class="search-bar" type="search" placeholder="Search...">
                    <button type="search" @click="search()" class="search-button">S</button>
                </div><br>
                <br>

                <div v-for="person in persons" :key="person._id" class="card my-4">

                    <div class="card">
                        <div class="card-body">

                            <ul class="list-group list-group-vertical">

                                <li class="list-group-item">
                                    <h2 class="card-title">{{ person.category }}</h2>
                                    <button class="popup-open-button" @click="openComment()">Yorum Yap</button>
                                </li>

                                <li class="list-group-item">
                                    <h5>{{ person.question }}</h5>
                                    <p class="date-text">{{ currentDate }},{{ currentTime }}</p>
                                </li>

                                <li class="list-group-item">{{ person.selectionOne }} <br>
                                    <button id="questionOneButton" class="question-average-button" @click="questionButton()"
                                        @dblclick="questionCloseButton()" type="button">
                                        <p id="numberTextOne" class="number-text"> %25 </p>
                                    </button>
                                </li>

                                <li class="list-group-item">{{ person.selectionTwo }} <br>
                                    <button id="questionTwoButton" class="question-average-button" @click="questionButton()"
                                        @dblclick="questionCloseButton()" type="button">
                                        <p id="numberTextTwo" class="number-text"> %25 </p>
                                    </button>
                                </li>

                                <li class="list-group-item">{{ person.selectionThree }} <br>
                                    <button id="questionThreeButton" class="question-average-button"
                                        @click="questionButton()" @dblclick="questionCloseButton()" type="button">
                                        <p id="numberTextThree" class="number-text"> %50 </p>
                                    </button>
                                </li>
                            </ul>

                            <br>

                            <button type="button" @click=" editPerson(person._id)" class="btn btn-primary"> Edit</button>
                            <button type="button" @click="removePerson(person._id)" class="btn btn-danger">Delete</button>

                        </div>
                    </div>
                </div>
            </div>

            <div class="col-sm-3">
                <div>
                    <CommentForm />
                </div>

            </div>
        </div>
    </div>
</template>

<script>
import router from "../router";
import axios from "axios";
import CommentForm from "../components/CommentForm.vue"
import SideBar from "../components/SideBar.vue"

export default {

    components: {
        SideBar,
        CommentForm,
    },

    data() {
        return {
            persons: [],
            currentDate: "",
            currentTime: ""
        }
    },

    created() {
        this.getPersons(),
            this.getCurrentDateTime(),
            this.getComment()
    },

    methods: {
       
        async getPersons() {
            try {
                const response = await axios.get('http://localhost:3000/questionnaire')
                this.persons = response.data

                


            } catch (error) {
                console.error(error)
            }
        },


        async removePerson(_id) {
            try {
                await axios.delete(`http://localhost:3000/questionnaire/${_id}`);
                this.getPersons();
            } catch (error) {
                console.log(error);
            }
        },

        editPerson(_id, selectionOne, selectionTwo, selectionThree, category) {
            try {
                const response = axios.get(`http://localhost:3000/questionnaire/${_id}`, { selectionOne, selectionTwo, selectionThree, category })
                this.response = response.data,

                    console.log(response),
                    router.replace({
                        path: `/questionnaire/${_id}`,
                    });
                    
            }
            catch (error) {
                console.log(error)
            }
        },

        

        search() {

            const searchQuery = document.querySelector(".search-bar").value.toLowerCase();

            // Listeyi filtrele ve kişileri getir
            const filteredPersons = this.persons.filter(person => {
                const category = person.question.toLowerCase();
                const question = person.question.toLowerCase();
                const selectionOne = person.selectionOne.toLowerCase();
                const selectionTwo = person.selectionTwo.toLowerCase();
                const selectionThree = person.selectionThree.toLowerCase();

                return (
                    question.includes(searchQuery) || selectionOne.includes(searchQuery) || selectionTwo.includes(searchQuery)
                    || selectionThree.includes(searchQuery) || category.includes(searchQuery)
                );
            });

            // Filtrenenleri güncelle
            this.persons = filteredPersons;

        },

        logout() {
            localStorage.clear()
            router.replace({
                path: "/",
            });
        },

        questionButton() {
            document.getElementById("questionOneButton").style.height = "5px";
            document.getElementById("questionTwoButton").style.height = "5px";
            document.getElementById("questionThreeButton").style.height = "5px";

            document.getElementById("numberTextOne").style.visibility = "visible";
            document.getElementById("numberTextTwo").style.visibility = "visible";
            document.getElementById("numberTextThree").style.visibility = "visible";
        },

        swipeTo() {
            document.getElementById("swipe-button").style.height = "320px";
        },

        getCurrentDateTime() {
            const date = new Date();
            this.currentDate = date.toDateString();
            this.currentTime = date.toLocaleTimeString();
        },

        openComment() {
            document.getElementById("comment-nav").style.visibility = "visible";
        },


    },
};

</script>

<style>
.search-bar {
    width: 540px;
    height: auto;
    border-radius: 10px;
    border-color: black;
    text-align: center;
    margin-left: 10px;
    margin-top: 9px;
}

.search-area {
    margin-bottom: 0;
    width: 615px;
    height: 50px;
    background-color: rgba(0, 0, 139, 0.137);
    z-index: 1;
    border-radius: 10px;
}

.search-button {
    width: 40px;
    height: 40px;
    margin-left: 9px;
    border-radius: 50px;
    border-color: dodgerblue;
}

.question-average-button {
    width: 530px;
    height: 34px;
    background-color: gray;
    border-color: black;
    border-width: 1px;
    transition: 0.5s;
    visibility: visible;

}

.question-average-button:hover {
    background-color: rgba(94, 85, 85, 0.493);
    border-color: black;
    border-width: 1px;
    border-radius: 10px;
}

.number-text {
    visibility: hidden;
    margin-top: 3px;
}

.date-text {
    font-size: 10px;
}

.popup-open-button {
    background-color: rgb(16, 214, 16);
    border-radius: 4px;
    color: white;
}

.popup-open-button:hover {
    background-color: rgba(0, 128, 0, 0.671);
}
</style>

