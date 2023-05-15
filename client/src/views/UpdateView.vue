<template>
    <div>

        <div>
            <SideBar/>
            
        </div>

        <div>

            <PersonForm />
        </div>
    </div>
</template>

<script>
import { ref } from "vue";
import PersonForm from "../components/PersonForm.vue"
import SideBar from "../components/SideBar.vue"
import PersonList from "../components/PersonList.vue";
import router from "../router";
import axios from "axios";

export default {

    components: {
        SideBar,
        PersonForm,

    },

    data() {

        const person = ref({
            age: '',
            country: '',
            city: '',
            message: '',
        })

    },

    methods: {
        getPersons() {
            try {
                const { _id } = this.$router.params
                const { age, country, city, message } = router.params
                const response = axios.get(`http://localhost:3000/persons/${_id, age, country, city, message}`, this.person)
                const json = response.json()
                person.value = json

            } catch (error) {
                console.error(error)
            }
        },

        updatePerson(_id) {
            try {
                const { _id } = this.$router.params
                const { age, country, city, message } = this.person
                const response = axios.put(`http://localhost:3000/update/${_id, age, country, city, message}`)
                const data = response.data

            } catch (error) {
                console.log(error)
            }
        },
    }

}

</script>