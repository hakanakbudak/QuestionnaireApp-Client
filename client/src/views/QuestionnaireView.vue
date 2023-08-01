<template>
    <div>
        <div>
          
        </div>
        <div>
            <QuestionnaireList/>
        </div>
    </div>
</template>
  
<script>
import QuestionnaireList from "@/components/QuestionnaireList.vue";
import axios from 'axios';
export default {
    components: {
        QuestionnaireList,
},
    data() {
        return {
            questionnaires: [],           
        };
    },
    created(){
        this.getPersons()
        
    },
    methods: {
        async getPersons() {
            try {
                const response = await axios.get(`http://localhost:3000/questionnaire`)
                this.questionnaires = response.data
                
                
               } catch (error) {
                   console.error(error)
               }
           },
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