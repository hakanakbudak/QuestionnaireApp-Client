<template>
    <div>
        <div class="row">
            <div class="col-sm-3">
                <div id="sideBar" :style="sideBarStyle" class="side-nav">
                    <table class="table-body">
                        <tr>
                            <td>
                                <div id="main"  class="open-side-bar">
                                    <span  @click="openSidebar()">
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
                                <img class="profile-image"
                                    src="https://www.gentas.com.tr/wp-content/uploads/2021/05/3190-siyah_renk_g483_1250x1000_t3cksofn.jpg">
                                <p class="profileUsername">bluesauer</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <button class="home-button" @click="goToHome()">Home Page</button><br>
                                <button class="home-button" @click="goToQuestionnaireCreate()">Create Questionnaire</button><br>
                                <button class="home-button" @click="goToMyQuestionnaire()">My Questionnaires</button><br>
                                <button class="home-button" @click="goToSetting()">Setting</button>    <br>
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
</template>

<script>

import router from "../router";
import axios from "axios";

export default {

    data(){
        return{
            sideBarStyle: {
                width:'width:250px',
                marginLeft:'marginLeft:250px'
            },
            
        }
    },

    
    methods: {
        openSidebar() {
            document.getElementById("sideBar").style.width = "250px";
            document.getElementById("main").style.marginLeft = "250px";
            //this.sideBarStyle.width = '250px';
            //this.sideBarStyle.marginLeft = '250px';
        },
        closeSidebar() {
            document.getElementById("sideBar").style.width = "0";
            document.getElementById("main").style.marginLeft = "0";
            //this.sideBarStyle.width = '0px';
            //this.sideBarStyle.marginLeft = '0px';
        },
        logoutButton() {
            localStorage.clear()
            router.replace({
                name: "Home",
            });
        },
        loginViewButton() {
            router.replace({
                path: "/questionnaire/:userId",
            });
        },
        goToHome(){
            router.replace({
                path:"/questionnaire"
            })

        },
        goToQuestionnaireCreate(){
            router.replace({
                path:"/questionnaire/create/:id"
            })
        },
        goToMyQuestionnaire(){
            router.replace({
               path:"/questionnaire/:userId"
            })
        },
        goToSetting(){
            router.replace({
                path:"/setting"
            })
        },
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
    position:fixed;
    z-index: 1;
    top: 0;
    left:0;
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
.profile-image {
    width: 100px;
    height: 100px;
    margin-top: 5px;
    margin-left: auto;
    margin-right: auto;
}
.logout-button {
    width: 150px;
    height: 50px;
    color: white;
    outline: 0;
    border: 2px solid currentcolor;
    border-color: darkslateblue;
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
.home-button {
    background-color: transparent;
    border-color: transparent;
    font-size: 20px;
}
.home-button :hover{
    background-color: transparent;
    border-color: transparent;
    font-size: 20px;
    color: aquamarine;
}
</style>