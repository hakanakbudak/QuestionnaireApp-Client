<template>
    <div class="container">
        <hr>

        <div v-for="person in persons" :key="person._id" class="card my-4">

            <div class="card">
                <div class="card-body">

                    <ul class="list-group list-group-vertical">


                        <li class="list-group-item">
                            <h2 class="card-title">{{ person.category }}</h2>
                        </li>

                        <li class="list-group-item">
                            <h5>{{ person.question }}</h5>
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
                            <button id="questionThreeButton" class="question-average-button" @click="questionButton()"
                                @dblclick="questionCloseButton()" type="button">
                                <p id="numberTextThree" class="number-text"> %50 </p>
                            </button>
                        </li>
                    </ul>

                    <br>

                    <button type="button" @click="editPerson(person._id)" class="btn btn-primary"> Edit
                    </button>
                    <button type="button" @click="removePerson(person._id)" class="btn btn-danger">Delete</button>



                </div>

            </div>



        </div>

    </div>
</template>

<script>
import router from "../router";
import axios from "axios";

export default {


    data() {
        return {
            persons: []
        }
    },

    created() {
        this.getPersons()
    },

    methods: {
        async getPersons() {
            try {
                const response = await axios.get('http://localhost:3000/persons')
                this.persons = response.data


            } catch (error) {
                console.error(error)
            }
        },
    },


};
</script>