<template>
    <PersonForm />
</template>

<script>
import PersonForm from "../components/PersonForm.vue"
import PersonList from "../components/PersonList.vue";
import router from "../router";
import axios from "axios";

export default {

    components: {
        PersonForm,

    },

    data() {
        return {
            person: {
                age: '',
                country: '',
                city: '',
                message: ''
            }
        }
    },

    methods: {
        async getPersons() {
            try {
                const { _id } = this.$router.params
                const { age, country, city, message } = router.params
                const response = await axios.get(`http://localhost:3000/persons/${_id,age, country, city, message}`, this.person)
                const data = await response.data

                this.person = data

            } catch (error) {
                console.error(error)
            }
        },

        async updatePerson(_id) {
            try {
                const { age, country, city } = this.person
                const response = await axios.put(`http://localhost:3000/update/${_id,age,country,city}`)
                const data = await response.data

                this.person = data
                    

            } catch (error) {
                console.log(error)
            }
            return {
                person,
                getPersons,
                updatePerson,
            }
        }

    }
}
</script>