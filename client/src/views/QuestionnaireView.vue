<template>
    <div>
        <div>
          
        </div>
        <div>
            <QuestionnaireList :questionnaires="questionnaires"/>
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
        this.getQuestionnaires()
        
    },
    methods: {
        async getQuestionnaires() {
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
                    this.person = res.data
                })
            } catch (error) {
                console.log(error)
            }
        },
    },
};
</script>