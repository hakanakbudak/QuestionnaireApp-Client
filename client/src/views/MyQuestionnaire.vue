<template>
    <div>
        <h1>{{ }}</h1>
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
                                    <Comment :questionnaireId="questionnaire._id"
                                            @someEvent="handleCommentEvent"></Comment>
                                </li>
                                <li class="list-group-item">
                                    <h5>{{ questionnaire.question }}</h5>
                                </li>

                                <li class="list-group-item">{{ questionnaire.selectionOne }} <br>

                                    <button id="questionOneButton" :style="buttonStyle" class="question-average-button"
                                        @click="handleSelection(1, questionnaire._id)" type="button">
                                        <p id="numberTextOne" v-if="isButtonShown" class="number-text">
                                            %{{ selectionARatio }}</p>
                                    </button>
                                </li>
                                <li class="list-group-item">{{ questionnaire.selectionTwo }} <br>
                                    <button id="questionTwoButton" :style="buttonStyle" class="question-average-button"
                                        @click="handleSelection(2, questionnaire._id)" type="button">
                                        <p id="numberTextTwo" v-if="isButtonShown" class="number-text">
                                            %{{ selectionBRatio }} </p>
                                    </button>
                                </li>
                                <li class="list-group-item">{{ questionnaire.selectionThree }} <br>
                                    <button id="questionThreeButton" :style="buttonStyle" class="question-average-button"
                                        @click="handleSelection(3, questionnaire._id)" type="button">
                                        <p id="numberTextThree" v-if="isButtonShown" class="number-text">
                                            %{{ selectionCRatio }} </p>
                                    </button>
                                </li>

                            </ul>
                            <br>
                            <div>
                                <button type="button" @click="editQuestionnaire(questionnaire._id)" class="btn-edit">
                                    Edit</button>
                                <button type="button" @click="openPopup(questionnaire._id)"
                                    class="btn-delete">Delete</button>
                                <div v-if="isPopupOpen" class="popup-overlay">
                                    <div class="popup-content">
                                        <h4 class="popup-title">{{ selectedQuestionnaireId }}</h4>
                                        <h6></h6>
                                        <p class="popup-text">Anketi silmek istediğinize emin misiniz?</p>
                                        <button class="popup-close-button" @click="closePopup()">No</button>
                                        <button class="popup-yes-button" @click="removeQuestionnaire()">Yes</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-sm-3">
                <div>
                    
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import router from "../router";
import axios from "axios";
import SideBar from "../components/SideBar.vue"
import Comment from "../components/Comment.vue";
import jwt_decode from "jwt-decode";
export default {
    
    components: {
        SideBar,
        Comment
        
    },

    props: {
        questionnaireId: {
            type: String,
            required: true,
            default: 0,
        },
    },
    
    data() {
        return {
            questionnaires: [],
            result: "",
            buttonStyle: {
                height: 'height:34px'
            },
            isButtonShown: false,
            searchQuery: '',
            isPopupOpen: false,
            selectedQuestionnaireId: null,
            isCommentShow: false,
            isCommentShow: false,
            selectedQuestionnaireId: null,
            questionnaire: null,
            selectionARatio: 0,
            selectionBRatio: 0,
            selectionCRatio: 0,
            surveyResults: {},
        }
    },
    created() {
        this.getMyQuestionnaires();
        this.getData();
        this.getSurveyResults();

    },
    methods: {
        getData() {
            axios
                .get("http://localhost:3000/getData", {
                    headers: {
                        "Access-Control-Allow-Origin": "*",
                        Accept: "application/json",
                        "Content-Type": "application/json",
                        Authorization: localStorage.access_token,
                    },
                    withCredentials: false,
                })
                .then(
                    (res) => {
                        this.result = res.data;
                        console.log("data get succesfully");
                    },
                    (error) => {
                        console.log(error);
                    }
                )
                .catch((e) => {
                    console.log(e);
                });
        },
        async getMyQuestionnaires() {
            try {
                const token = localStorage.getItem("access_token");
                const decodedToken = jwt_decode(token);
                const userId = decodedToken._id;
                const response = await axios.get(`http://localhost:3000/questionnaire/${userId}`);
                this.questionnaires = response.data;
                router.replace({
                    path: `/questionnaire/${userId}`,
                });
            } catch (error) {
                console.log(error);
            }
        },
        async removeQuestionnaire() {
            try {
                await axios.delete(`http://localhost:3000/questionnaire/${this.selectedQuestionnaireId}`);
                this.getMyQuestionnaires();
                this.isPopupOpen = false;
                this.selectedQuestionnaireId = null;
            } catch (error) {
                console.log(error);
            }
        },

        openPopup(_id) {
            this.selectedQuestionnaireId = _id;
            this.isPopupOpen = true;
        },

        closePopup() {
            this.isPopupOpen = false;
        },
        
        editQuestionnaire(_id, selectionOne, selectionTwo, selectionThree, category, questionnaireDate) {
            try {
                const response = axios.get(`http://localhost:3000/questionnaire/${_id}`, { selectionOne, selectionTwo, selectionThree, category, questionnaireDate })
                this.response = response.data,
                    console.log(response),
                    router.replace({
                        path: `/questionnaire/update/${_id}`,
                    });

            }
            catch (error) {
                console.log(error)
            }
        },
        searchQuestionnaire() {
            axios.get('http://localhost:3000/search', { params: { searchQuery: this.searchQuery } })
                .then(response => {
                    this.questionnaires = response.data
                    console.log(response.data);
                })
                .catch(error => {
                    console.error(error);
                });
        },

        questionButton() {
            this.buttonStyle.height = '5px';
            this.isButtonShown = true;
        },    

        async handleCommentEvent(questionnaireId) {
            this.isCommentShow = !this.isCommentShow;
            this.selectedQuestionnaireId = questionnaireId;
            await this.getComment(questionnaireId);
        },


        async handleSelection(selectionId, questionnaireId) {
            try {
                this.selectedQuestionnaireId = questionnaireId;
                const token = localStorage.getItem("access_token");
                const decodedToken = jwt_decode(token);
                const userId = decodedToken._id;
                console.log(token)
                await axios.post("http://localhost:3000/submitVote", { selectionId, questionnaireId, userId });
                this.getSurveyResults(questionnaireId);
            } catch (error) {
                console.error(error);
            }
        },
        async getSurveyResults() {
            try {
                const response = await axios.get("http://localhost:3000/getSurveyResults");
                this.selectionARatio = response.data.selectionARatio;
                this.selectionBRatio = response.data.selectionBRatio;
                this.selectionCRatio = response.data.selectionCRatio;
            } catch (error) {
                console.error(error);
            }
        },
    }
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

.btn-edit {
    width: 280px;
    height: 30px;
    background-color: rgb(16, 214, 16);
    border-radius: 5px;
}

.btn-edit :hover {
    width: 280px;
    height: 30px;
    background-color: rgb(16, 214, 16);
    border-radius: 5px;
}


.btn-delete {
    width: 285px;
    height: 30px;
    background-color: red;
    border-radius: 5px;
    margin-left: 1px;
}

.btn-delete:hover {
    width: 285px;
    height: 30px;
    background-color: red;
    border-radius: 5px;
    margin-left: 1px;
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

