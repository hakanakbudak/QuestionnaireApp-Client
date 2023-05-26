<template>
    <div class="container contact-form">

        <form method="post">

            <div class="row">

                <div class="col-md-5">

                    <div id="comment-nav" class="comment-nav">

                        <div id="comment-list-close" class="comment-body">
                            <div class="close-button-position">
                                <button type="button" class="comment-button-close" @click="commentClose()">Close</button>
                            </div>
                            <br>
                            
                            <div v-for="comments in comment" :key="comments._id">
                                <div>
                                    <p>{{ comments.comment }}</p>
                                    
                                </div>
                            </div>

                        </div>

                        <div id="comment-button-close">

                            <input type="text" v-model="commented.comment" class="comment-input-send"
                                value="commented.comment" placeholder="  comment..">
                            <button type="button" class="comment-button-send" @click="commentSend()">Send</button>
                        </div>

                    </div>

                </div>

            </div>
        </form>
    </div>
</template>

<script>
import router from "../router";
import axios from "axios";
export default {

    data() {
        return {
            comment: [],
            commented: {
                comment: "",
            },
        };
    },

    created() {
        this.getComment()
    },

    methods: {
        commentSend() {
            try {
                axios
                    .post("http://localhost:3000/comment", this.commented, {})
                    .then((response) => {
                        console.log(response);
                        this.getComment()

                    })
                    .catch((error) => {
                        console.log(error);
                    });
            } catch (error) {
                console.log(error);
            }
        },

        async getComment() {
            try {
                const commentResponse = await axios.get('http://localhost:3000/comment')
                this.comment = commentResponse.data
            } catch (error) {
                console.error(error)
            }
        },

        commentClose() {
            document.getElementById("comment-nav").style.visibility = "hidden";
            document.getElementById("comment-list-close").style.visibility = "hidden";
            document.getElementById("comment-button-close").style.visibility = "hidden";
        }
    },
};
</script>

<style>
.comment-nav {
    height: 10px;
    width: 10px;
    position: fixed;
    z-index: 1;
    overflow-x: hidden;
    transition: 0.5s;
    padding-top: 60px;
    visibility: hidden;

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
    overflow-x: hidden;

}

.comment-list {}

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
}</style>