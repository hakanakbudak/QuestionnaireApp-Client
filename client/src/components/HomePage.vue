<template>
     <div class="container">
        <hr>
        <div v-for="person in persons" :key="person._id" class="card my-2">

            <div class="card">
                <div class="card-body">
                    <h5 class="card-title">User Info</h5>

                    <ul class="list-group list-group-vertical">
                        <li class="list-group-item">{{ person.age }}</li>
                        <li class="list-group-item">{{ person.country }}</li>
                        <li class="list-group-item">{{ person.city }}</li>
                        <li class="list-group-item">{{ person.message }}</li>
                    </ul>
                    <br>

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