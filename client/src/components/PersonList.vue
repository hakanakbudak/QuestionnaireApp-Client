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

                    <button type="button" @click="editPerson(person._id)" class="btn btn-primary"> Edit </button>
                    <button type="button" @click="removePerson(person._id)" class="btn text-white "
                        style="background-color: red;">Delete</button>

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


        async removePerson(_id) {
            try {
                await axios.delete(`http://localhost:3000/persons/${_id}`);
                this.getPersons();
            } catch (error) {
                console.log(error);
            }
        },


        async editPerson(_id, age, country, city) {
            try {
                const response = axios.put(`http://localhost:3000/update/${_id}`, { age, country, city })
                this.response = response.data,

                    console.log(response),
                    router.replace({
                        path: `/update/${_id}`,
                    });

            }
            catch (error) {
                console.log(error)
            }
            return {
                persons,
                removePerson,
                updatePerson

            }

        },

    }
};

</script>