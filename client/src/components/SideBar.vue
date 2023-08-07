<template>
    <div>
        <div class="row">
            <div class="col-sm-3">
                <div class="main-content">
                <div id="sideBar" :style="sideBarStyle" class="side-nav">
                    <table class="table-body">
                        <tr>
                            <td>
                                <div id="main" class="open-side-bar">
                                    <span @click="openSidebar()">
                                        &#9776;
                                    </span>
                                </div>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <a href="javascript:void(0)" class="close-side-bar" @click="closeSidebar()">

                                    &times;</a>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <img class="app-icon" src="https://cdn-icons-png.flaticon.com/512/1169/1169549.png">
                                <p class="profileUsername">{{ userName }}</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <button class="menu-button" @click="goToHome()">Home Page</button><br>
                                <button class="menu-button" @click="goToQuestionnaireCreate()">Create
                                    Questionnaire</button><br>
                                <button class="menu-button" @click="goToMyQuestionnaire()">My Questionnaires</button><br>
                                <button class="menu-button" @click="goToSetting()">Setting</button> <br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <button type="button" @click="logoutButton()" class="logout-button">Logout</button>

                            </td>
                        </tr>
                        <br>
                    </table>
                </div>
            </div>
            </div>
        </div>
    </div>
</template>

<script>

import router from "../router";
import axios from "axios";
import jwt_decode from "jwt-decode";


export default {

    data() {
        return {
            sideBarStyle: {
                width: 'width:250px',
                marginLeft: 'marginLeft:250px'
            },
            userName: ""
        }
    },

    created() {
        this.getUserName()
    },

    methods: {
        openSidebar() {
            this.sideBarStyle.width = '250px';
            this.sideBarStyle.marginLeft = '250px';
        },
        closeSidebar() {
            this.sideBarStyle.width = '0px';
            this.sideBarStyle.marginLeft = '0px';
        },
        logoutButton() {
            localStorage.clear()
            router.replace({
                name: "Home",
            });
        },
        loginViewButton() {
            router.replace({
                path: "/questionnaire",
            });
        },
        goToHome() {
            router.replace({
                path: "/questionnaire"
            })

        },
        goToQuestionnaireCreate() {
            router.replace({
                path: "/questionnaire/create/:id"
            })
        },
        goToMyQuestionnaire() {
            router.replace({
                path: "/questionnaire/:userId"
            })
        },
        goToSetting() {
            router.replace({
                path: "/setting"
            })
        },

        getUserName() {
            const token = localStorage.getItem("access_token");
            const decodedToken = jwt_decode(token);
            const userId = decodedToken._id;
            this.userName = userId
        }
    }
}
</script>

<style>
body {
    border-top-left-radius: 100px;
}

.side-nav {
    height: 900px;
    width: 0;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: rgb(0, 9, 121, 1);
    overflow-x: hidden;
    transition: 0.5s;
    padding-top: 60px;
}

.side-nav a {
    padding: 1px 1px 5px 6px;
    text-decoration: none;
    font-size: 25px;
    color: white;
    display: block;
}

.side-nav a:hover {
    color: rgb(236, 146, 21);
}

.side-nav .close-side-bar {
    position: absolute;
    top: 0;
    right: 25px;
    font-size: 36px;
    margin-left: 50px;
}

.main-content{
    padding-left: 0;
    left: 0;
}

#main {
    transition: margin-left .5s;
    padding: 16px;
    background-color: rgba(220, 220, 220, 0.726);
    width: 60px;
    height: 70px;
}

@media screen and (max-height: 450px) {
    .side-nav {
        padding-top: 15px;
    }

    .side-nav a {
        font-size: 18px;
    }
}

.open-side-bar {
    font-size: 30px;
    cursor: pointer;
    position: fixed;
}

.table-body {
    margin-left: auto;
    margin-right: auto;
}

.app-icon {
    width: 150px;
    height: 150px;
    margin-top: 5px;
    margin-left: 25px;
    margin-right: auto;
    border-image: 20px;
    border-radius: 10px;
    border: 1px solid dodgerblue;
}

.logout-button {
    width: 200px;
    height: 50px;
    color: white;
    outline: 0;
    border: 2px solid currentcolor;
    border-color: cornflowerblue;
    transition: 0.3s ease all;
    background-color: rgba(71, 61, 139, 0.705);
    font-size: 15px;
    font-weight: 600;
    padding: 6px 15px;
    display: inline-block;
}

.logout-button:hover {
    color: white;
    border-color: transparent;
    background-color: dodgerblue;
    border-radius: 8px;
}

.profileUsername {
    color: aliceblue;
}

.menu-button {
    background-color: transparent;
    border-color: transparent;
    color: whitesmoke;
}

.menu-button:hover {
    background-color: dodgerblue;
}
</style>