<template>
    <div>
        <div>
            <button class="popup-open-button" @click="triggerSomeEvent()">
                Yorum Yap</button>
        </div>

        <div>
            <br>
            <div v-show="isCommentShow">
                <div class="comment-screen-body">
                    <div v-for="comment in comment" :key="comment._id">
                        <div>
                            <table class="table-body">
                                <tr>
                                    <div class="show-delete">

                                        <th>{{ comment.userId }}</th><span></span>
                                        <td>
                                           
                                            <p v-if="editingCommentId !== comment._id">{{ comment.comment }}</p>
                                            <input v-else v-model="comment.comment" class="edit-input">
                                            <button @click="startEdit(comment._id)" class="edit-button">Edit</button>

                                            <button v-if="editingCommentId === comment._id"
                                            @click="updateComment(questionnaireId, comment._id)"
                                            class="update-button">Update</button>
                                            <span> </span>
                                        <button @click="commentDelete(questionnaireId, comment._id)"
                                            class="deleted-button">Delete</button>
                                        </td>
                                    </div>
                                </tr>
                            </table><br>
                        </div>
                    </div>
                </div>

                <div>
                    <div class="input-and-send-body">
                        <input type="text" v-model="commented.comment" class="comment-input" placeholder="  comment..">
                        <button type="button" class="comment-input-send" @click="commentSend(questionnaireId)">Send</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import router from "../router";
import axios from "axios";
import QuestionnaireList from "@/components/QuestionnaireList.vue"
import jwt_decode from "jwt-decode";

export default {
    components: {
        QuestionnaireList
    },

    props: {
        questionnaireId: String,
    },

    data() {
        return {
            selectedQuestionnaireId: null,
            isCommentShow: false,
            comment: [],
            commented: {
                comment: "",
            },
            editingCommentId: null,
        }
    },

    methods: {
        async triggerSomeEvent(questionnaireId) {
            this.$emit("someEvent", this.questionnaireId);
            this.isCommentShow = !this.isCommentShow;
            await this.getComment(this.questionnaireId);
        },

        async getQuestionnaire() {
            try {
                const response = await axios.get(`http://localhost:3000/questionnaire`)
                this.questionnaires = response.data
            } catch (error) {
                console.error(error)
            }
        },

        async getComment(questionnaireId) {
            try {
                this.selectedQuestionnaireId = questionnaireId;
                const commentResponse = await axios.get(`http://localhost:3000/questionnaire/${questionnaireId}/comment`);
                this.comment = commentResponse.data;
            } catch (error) {
                console.error(error);
            }
        },

        commentSend() {
            try {
                const questionnaireId = this.selectedQuestionnaireId
                const token = localStorage.getItem("access_token");
                const decodedToken = jwt_decode(token);
                const userId = decodedToken._id;
                axios.post(`http://localhost:3000/questionnaire/comment/${userId}/${questionnaireId}`, { comment: this.commented.comment })
                    .then((response) => {
                        this.getComment(questionnaireId);
                        this.commented.comment = ""
                    })
                    .catch((error) => {
                        console.log(error);
                    });
                return
            } catch (error) {
                console.log(error);
            }
        },

        async commentDelete(questionnaireId, _id) {
            try {
                const response = await axios.delete(`http://localhost:3000/questionnaire/comment/${_id}`);
                console.log(response.data.message);
                await this.getComment(questionnaireId)
            } catch (error) {
                console.error(error);
            }
        },

        startEdit(_id) {
            this.editingCommentId = _id;
        },

        async updateComment(questionnaireId, _id) {
            try {
                const commentToUpdate = this.comment.find(comment => comment._id === _id);
                if (!commentToUpdate) {
                    console.error('Comment not found');
                    return;
                }

                const response = await axios.put(`http://localhost:3000/questionnaire/comment/${_id}`, {
                    comment: commentToUpdate.comment,
                });
                this.editingCommentId = null;
                await this.getComment(questionnaireId);
            } catch (error) {
                console.error(error);
            }
        },

    }
}
</script>

<style>
.comment-screen-body {
    width: 500px;
    height: 300px;
    background-color: white;
    border: 1px solid;
    border-color: black;

    overflow: scroll;
    scrollbar-width: thin;
}

.table-body {
    margin-left: 10px;
}

.input-and-send-body {
    margin-top: 10px;
}

.comment-input {
    width: 410px;
    background-color: transparent;
}

.comment-input-send {
    width: 80px;
    margin-left: 10px;
    background-color: rgb(16, 214, 16);
}

.comment-input-send:hover {
    background-color: rgb(231, 194, 94);
}

.popup-open-button {
    background-color: rgb(16, 108, 214);
    border-radius: 4px;
    color: white;
}

.popup-open-button:hover {
    background-color: rgba(0, 128, 0, 0.671);
}

.deleted-button {
    background-color: rgb(236, 99, 99);
    border-radius: 10px ;
}
.update-button{
    background-color: rgb(85, 154, 233);
    border-radius: 10px ;
}
.edit-button{
    background-color:darkorange;
    border-radius: 10px ;
}
</style>