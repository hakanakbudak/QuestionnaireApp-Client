<template>
    
    <div class="container contact-form">

        <form method="post">
            <div class="row">

                <div class="col-md-3">

                </div>

                <div class="col-md-5">

                </div>

                <div class="col-md-3">

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
            commentText: {
                comments: "",
            },
        };
    },

    methods: {
        commentSend() {
            axios
                .post("http://localhost:3000/comment", this.comments, {

                })
                .then(
                    (response) => {
                        console.log(response);
                    },
                    (error) => {
                        console.log(error);
                    }
                );
        },
    },
};
</script>

<style>

</style>