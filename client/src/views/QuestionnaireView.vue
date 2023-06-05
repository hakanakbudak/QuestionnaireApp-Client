<template>
    <div>
        <div>
            <SideBar />
        </div>

        <div>

            <PersonForm />
        </div>

    </div>
</template>
  
<script>
import SideBar from "../components/SideBar.vue"
import CreateForm from "../components/CreateForm.vue"
import PersonForm from "../components/PersonForm.vue"
import axios from 'axios';



export default {
    components: {
        SideBar,
        PersonForm,
        CreateForm,
    },

    data() {
        return {
            person: {
                category: "",
                selectionOne: "",
                selectionTwo: "",
                selectionThree: "",
                question: "",
            },
        };
    },

    created(){
        this.getData()
    },

    methods: {
        
        /*
        create() {
            axios
            .post("http://localhost:3000/questionnaire", this.person, {
                headers: {
                    "Access-Control-Allow-Origin": "http://localhost:3000/questionnaire",
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

            */
           

        updatePerson(_id) {
            try {
                const { selectionOne, selectionTwo, selectionThree, question } = this.person
                const response = axios.put(`http://localhost:3000/questionnaire/${_id, selectionOne, selectionTwo, selectionThree, question}`)


                response.then((res) => {
                    this.person = res.data // response'dan gelen veriyi person veri modeline atayın
                })
            } catch (error) {
                console.log(error)
            }
        },


    },


};
</script>