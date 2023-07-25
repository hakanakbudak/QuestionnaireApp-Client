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
                                    <button class="popup-open-button" @click="openComment(questionnaire._id)">Yorum
                                        Yap</button>
                                </li>
                                <li class="list-group-item">
                                    <h5>{{ questionnaire.question }}</h5>
                                    <p class="question-shared-date">Question shared date : {{
                                        questionnaire.questionnaireDate }}</p>
                                </li>
                                <li class="list-group-item">{{ questionnaire.selectionOne }} <br>

                                    <button id="questionOneButton" :style="buttonStyle" class="question-average-button"
                                        @click="handleSelection(1, questionnaire._id)" type="button" value="1">
                                        <p id="numberTextOne" class="number-text">
                                            %{{ selectionARatio }} </p>
                                    </button>

                                </li>
                                <li class="list-group-item">{{ questionnaire.selectionTwo }} <br>
                                    <button id="questionTwoButton" :style="buttonStyle" class="question-average-button"
                                        @click="handleSelection(2, questionnaire._id)" type="button">
                                        <p id="numberTextTwo" class="number-text">
                                            %{{ selectionBRatio }} </p>
                                    </button>
                                </li>
                                <li class="list-group-item">{{ questionnaire.selectionThree }} <br>
                                    <button id="questionThreeButton" :style="buttonStyle" class="question-average-button"
                                        @click="handleSelection(3, questionnaire._id)" type="button">
                                        <p id="numberTextThree" class="number-text">
                                            %{{ selectionCRatio }} </p>
                                    </button>
                                </li>
                            </ul>
                            <br>
                            <div>
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
                    <div class="container contact-form">
                        <form method="post">
                            <div class="row">
                                <div class="col-md-5" v-show="isCommentShow">
                                    <div id="comment-nav" class="comment-nav">
                                        <div id="comment-list-close" class="comment-body">
                                            <div class="close-button-position">
                                            </div>
                                            <br>
                                            <div v-for="comment in comment" :key="comment._id">
                                                <div>
                                                    {{ comment.comment }}
                                                </div>
                                            </div>
                                        </div>
                                        <div id="comment-button-close">
                                            <input type="text" v-model="commented.comment" class="comment-input-send"
                                                placeholder="  comment..">
                                            <button type="button" class="comment-button-send"
                                                @click="commentSend(questionnaire._id)">Send</button>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import router from "../router";
import axios from "axios";
import SideBar from "../components/SideBar.vue"
import jwt_decode from "jwt-decode";

export default {
    components: {
        SideBar,
    },
    data() {
        return {
            questionnaires: [],
            questionnaireDate: "",
            questionnaireId: "",
            buttonStyle: {
                height: 'height:34px'
            },
            isButtonShown: false,
            searchQuery: '',
            isPopupOpen: false,
            selectedQuestionnaireId: null,
            isCommentShow: false,
            comment: [],
            commented: {
                comment: "",
            },
            isCommentShow: false,
            selectedQuestionnaireId: null,
            selectionARatio: 0,
            selectionBRatio: 0,
            selectionCRatio: 0,
        }
    },
    created() {
        this.getQuestionnaire();
        this.getSurveyResults();
    },
    methods: {
        async getQuestionnaire() {
            try {
                const response = await axios.get(`http://localhost:3000/questionnaire`)
                this.questionnaires = response.data
            } catch (error) {
                console.error(error)
            }
        },
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
        commentSend(questionnaireId) {
            this.selectedQuestionnaireId = questionnaireId;
            try {
                axios.post(`http://localhost:3000/questionnaire/comment/${questionnaireId}`, { comment: this.commented })
                    .then((response) => {
                        console.log(response);
                        this.openComment()
                    })
                    .catch((error) => {
                        console.log(error);
                    });
                return
            } catch (error) {
                console.log(error);
            }
        },
        async openComment(questionnaireId) {
            this.isCommentShow = !this.isCommentShow;
            this.selectedQuestionnaireId = questionnaireId;
            try {
                const commentResponse = await axios.get(`http://localhost:3000/questionnaire/${questionnaireId}/comment`);
                this.comment = commentResponse.data;
            } catch (error) {
                console.error(error);
            }
        },
        commentClose() {
            this.isCommentShow = false;
        },
        async handleSelection(selectionId, questionnaireId) {
            try {
                this.selectedQuestionnaireId = questionnaireId;
                const token = localStorage.getItem("access_token");
                const decodedToken = jwt_decode(token);
                const userId = decodedToken._id;
                console.log(token)
                await axios.post("http://localhost:3000/submitVote", { selectionId, questionnaireId, userId });
                this.getSurveyResults();
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

.question-shared-date {
    font-size: 10px;
}















.comment-nav {
    height: 10px;
    width: 10px;
    position: fixed;
    z-index: 1;
    overflow-x: visible;
    transition: 0.5s;
    padding-top: 60px;

    visibility: visible;

}

.comment-body {
    width: 350px;
    height: 350px;
    background-color: white;
    border: 2px solid;
    border-color: black;
    position: fixed;
    bottom: 40px;
    border-radius: 5px;

    overflow: scroll;
    scrollbar-width: thin;

    overflow-x: visible;

}

.comment-input-send {
    width: 260px;
    height: 30px;
    position: fixed;
    bottom: 3px;
    margin-left: 3px;
    border-radius: 15px;
}

.comment-button-send {
    width: 60px;
    height: 30px;
    background-color: rgba(16, 214, 16, 0.649);
    position: fixed;
    bottom: 3px;
    right: 143px;
    border-radius: 15px;
}

.comment-button-send:hover {
    background-color: rgb(16, 214, 16);
    color: white;
}

.comment-button-close {
    width: 330px;
    height: 30px;
    top: 0px;
    background-color: rgb(226, 5, 5);
    border-radius: 4px;
    border-color: white;
}

.comment-button-close:hover {
    background-color: red;
    color: white;
    width: 333px;
    height: 33px;

}

.close-button-position {
    position: fixed;
}
</style>

