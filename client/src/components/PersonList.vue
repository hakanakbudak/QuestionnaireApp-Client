<template>
    <div>
        <SideBar />
        <div class="row">

            <div class="col-sm-3">

            </div>

            <div class="col-sm-5">
                <br>
                <div class="search-area">
                    <input class="search-bar" v-model="searchQuery" type="search" placeholder="Search...">
                    <button type="search" @click="searchQuestionnaire()" class="search-button">S</button>
                </div>

                <div v-for="questionnaire in questionnaires" :key="questionnaire._id" class="card my-4">

                    <div class="card">
                        <div class="card-body">

                            <ul class="list-group list-group-vertical">

                                <li class="list-group-item">
                                    <h2 class="card-title">{{ questionnaire.category }}</h2>
                                    <button class="popup-open-button" @click="openComment()">Yorum Yap</button>
                                </li>

                                <li class="list-group-item">
                                    <h5>{{ questionnaire.question }}</h5>
                                    <p class="date-text">{{ currentDate }},{{ currentTime }}</p>
                                </li>

                                <li class="list-group-item">{{ questionnaire.selectionOne }} <br>

                                    <button id="questionOneButton" :style="buttonStyle" class="question-average-button"
                                        @click="questionButton()" type="button">
                                        <p id="numberTextOne" v-if="isButtonShown" class="number-text"> %25 </p>
                                    </button>

                                </li>

                                <li class="list-group-item">{{ questionnaire.selectionTwo }} <br>
                                    <button id="questionTwoButton" :style="buttonStyle" class="question-average-button"
                                        @click="questionButton()" type="button">
                                        <p id="numberTextTwo" v-if="isButtonShown" class="number-text"> %25 </p>
                                    </button>
                                </li>

                                <li class="list-group-item">{{ questionnaire.selectionThree }} <br>
                                    <button id="questionThreeButton" :style="buttonStyle" class="question-average-button"
                                        @click="questionButton()" type="button">
                                        <p id="numberTextThree" v-if="isButtonShown" class="number-text"> %50 </p>
                                    </button>
                                </li>

                            </ul>

                            <br>


                            <div>
                                <button type="button" @click="editQuestionnaire(questionnaire._id)" class="btn btn-primary">
                                    Edit</button>

                                <button type="button" @click="openPopup(questionnaire._id)"
                                    class="btn btn-danger">Delete</button>

                                <div v-if="isPopupOpen" class="popup-overlay">
                                    <div class="popup-content">
                                        <h4 class="popup-title">{{ selectedQuestionnaireId }}</h4>
                                        <h6></h6>
                                        <p class="popup-text">Anketi silmek istediğinize emin misiniz?</p>
                                        <button class="popup-close-button" @click="closePopup()">No</button>
                                        <button class="popup-yes-button" @click="removeQuestionnaire">Yes</button>
                                    </div>
                                </div>
                            </div>

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
            questionnaires: [],
            currentDate: "",
            currentTime: "",
            buttonStyle: {
                height: 'height:34px'
            },
            isButtonShown: false,
            searchQuery: '',
            isPopupOpen: false,
            selectedQuestionnaireId: null,
        }
    },

    created() {
        this.getPersons(),
            this.getCurrentDateTime(),
            this.getComment(),
            this.getData()
    },

    methods: {

        async getPersons() {
            try {
                const response = await axios.get('http://localhost:3000/questionnaire',)
                this.questionnaires = response.data


            } catch (error) {
                console.error(error)
            }
        },

        /**
        *  Seçmiş olduğumuz ankete _id'si üzerinden delete isteği yapıyorum ve anketi siliyorum.
        *  @author Hakan Akbudak
       **/
        async removeQuestionnaire() {
            try {
                await axios.delete(`http://localhost:3000/questionnaire/${this.selectedQuestionnaireId}`);
                this.getPersons();
                this.isPopupOpen = false;
                this.selectedQuestionnaireId = null;
            } catch (error) {
                console.log(error);
            }
        },

        /** 
        * Delete butonu için popup open button
        **/
        openPopup(_id) {
            this.selectedQuestionnaireId = _id;
            this.isPopupOpen = true;
        },

        /** 
        * Delete butonu için popup close button
        **/
        closePopup() {
            this.isPopupOpen = false;
        },

        /**
         *  Seçmiş olduğumuz ankete _id'si üzerinden get isteği yapıyorum ve anket bilgilerini çekiyorum.
         *  @author Hakan Akbudak
        **/
        editQuestionnaire(_id, selectionOne, selectionTwo, selectionThree, category) {
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

        /**
         * Search işlemini server tarafında gerçekleştiriyorum.
         *  @author Hakan Akbudak
        **/
        searchQuestionnaire() {
            axios.get('http://localhost:3000/search', { params: { searchQuery: this.searchQuery } })
                .then(response => {
                    // Arama sonuçlarını işleyin
                    this.questionnaires = response.data
                    console.log(response.data);
                })
                .catch(error => {
                    // Hata durumunda işleme geçin
                    console.error(error);
                });
        },

        /**
         * Search işlemini Vuejs üzerinden gerçekleştiriyorum.
         *  @author Hakan Akbudak
        **/
        /*searchQuestionnaire() {
 
            const processedQuery = this.searchQuery.toLowerCase();
            //const searchQuery = document.querySelector(".search-bar").value.toLowerCase();
 
            // Listeyi filtrele ve kişileri getir
            const filteredQuestionnaires = this.questionnaires.filter(questionnaire => {
                const category = questionnaire.question.toLowerCase();
                const question = questionnaire.question.toLowerCase();
                const selectionOne = questionnaire.selectionOne.toLowerCase();
                const selectionTwo = questionnaire.selectionTwo.toLowerCase();
                const selectionThree = questionnaire.selectionThree.toLowerCase();
 
                return (
                    question.includes(processedQuery) || selectionOne.includes(processedQuery) || selectionTwo.includes(processedQuery)
                    || selectionThree.includes(processedQuery) || category.includes(processedQuery)
                );
            });

            // Filtrenenleri güncelle
            this.questionnaires = filteredQuestionnaires;
 
        },*/

        /**
         * (localStorage) alanını temizlemeyi gerçekleştiriyorum.
         *  @author Hakan Akbudak
        **/
        logout() {
            localStorage.clear()
            router.replace({
                path: "/",
            });
        },

        /**
         *   v-if="isButtonShown" kullanarak style değişikliği yapıyorum.
         *  @author Hakan Akbudak
        **/
        questionButton() {
            this.buttonStyle.height = '5px';
            this.isButtonShown = true;
        },

        /**
         *  Anketlerin paylaşım saatini tutuyorm.
         *  @author Hakan Akbudak
        **/
        getCurrentDateTime() {
            const date = new Date();
            this.currentDate = date.toDateString();
            this.currentTime = date.toLocaleTimeString();
        },

        /**
         *  Comment ekranını visible yapıyorum.
         *  @author Hakan Akbudak
        **/
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
    visibility: visible;
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






.popup-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 4;
}

.popup-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
    z-index: 4;
}

.popup-content h2 {
    margin-top: 0;
    z-index: 4;
}

.popup-content p {
    margin-bottom: 20px;
    z-index: 4;
}

.popup-content button {
    padding: 10px 20px;

    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    z-index: 4;
}

.popup-open-button {
    background-color: rgb(16, 214, 16);
    border-radius: 4px;
    color: white;
}

.popup-open-button:hover {
    background-color: rgba(0, 128, 0, 0.671);
}

.popup-close-button {
    background-color: rgb(212, 22, 22);
}

.popup-close-button:hover {
    border-width: 2px;
    background-color: rgba(212, 22, 22, 0.762);
}

.popup-yes-button {
    background-color: rgb(16, 214, 16);
}

.popup-yes-button:hover {
    background-color: rgba(16, 214, 16, 0.763);
}
</style>

