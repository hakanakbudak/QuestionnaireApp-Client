<template>
    <div>

        <div class="row">
            <div class="col-sm-3">
                <div id="YanMenu" class="sidenav">

                    <table class="tableOne">
                        <tr>
                            <td>
                                <div style="position: fixed;" id="main" class="openBtn">
                                    <span style="font-size:30px;cursor:pointer" @click="openNav()">

                                        &#9776; </span>

                                </div>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <a href="javascript:void(0)" class="closebtn" @click="closeNav()">

                                    &times;</a>
                            </td>
                        </tr>
                        <tr>
                            <td>

                                <img class="profileImg"
                                    src="https://www.gentas.com.tr/wp-content/uploads/2021/05/3190-siyah_renk_g483_1250x1000_t3cksofn.jpg">
                                <p class="profileUsername">bluesauer</p>

                            </td>
                        </tr>
                        <tr>
                            <td>
                                <a href="http://localhost:8080/">Home</a>
                                <a href="http://localhost:8080/create">Create</a>
                                <a href="http://localhost:8080/openpage">List</a>
                                <a href="http://localhost:8080/setting">Setting</a>
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
                                <button type="button" @click="logout()" class="logBtn">Logout</button>
                                
                            </td>
                    </tr>
                    <br>
                        <tr>
                            <td>
                                <ThemeButton/>
                            </td>
                        </tr>
                    </table>


                </div>
            </div>
        </div>
    </div>
</template>

<script>


import router from "../router";
import axios from "axios";
import ThemeButton from "@/components/ThemeButton.vue";


export default {

    components: {
        ThemeButton
    },
    
    methods: {
        openNav() {
            document.getElementById("YanMenu").style.width = "250px";
            document.getElementById("main").style.marginLeft = "250px";
        },

        closeNav() {
            document.getElementById("YanMenu").style.width = "0";
            document.getElementById("main").style.marginLeft = "0";
        },


        logout() {
            localStorage.clear()
            router.replace({
                path: "/",
            });
        },
    }
}

</script>

<style>
body {
    border-top-left-radius: 100px;
}

:root {
  --background-color-primary: #ebebeb;
  --background-color-secondary: #fafafa;
  --accent-color: #cacaca;
  --text-primary-color: #222;
  --element-size: 4rem;
}

/* Define styles for the root window with dark - mode preference */
:root.dark-theme {
  --background-color-primary: #1e1e1e;
  --background-color-secondary: #2d2d30;
  --accent-color: #3f3f3f;
  --text-primary-color: #ddd;
}


.sidenav {
    /*margin-top: 55px;*/
    height: 900px;
    width: 0;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    /* background: linear-gradient(to top, rgb(2, 9, 121, 1) 20%, rgb(0, 212, 255, 1) 45%, rgb(0, 9, 121, 1) 100%);*/
    background-color: rgb(0, 9, 121, 1);
    overflow-x: hidden;
    transition: 0.5s;
    padding-top: 60px;
}


.sidenav a {
    padding: 1px 1px 5px 6px;
    text-decoration: none;
    font-size: 25px;
    color: white;
    display: block;

}

.sidenav a:hover {
    color: darkblue;
}

.sidenav .closebtn {
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
    .sidenav {
        padding-top: 15px;
    }

    .sidenav a {
        font-size: 18px;
    }
}


.searchBar {
    width: 880px;
    height: 40px;
    border-radius: 10px;
    border-color: rgba(0, 0, 0, 0.282);
    text-align: center;
}

.searchBtn {
    height: 35px;
    width: 35px;
    padding-bottom: 9px;
    margin-left: 5px;
    border-radius: 10px;
    border-color: black;
    background-color: aqua;

}

.tableOne {
    margin-left: auto;
    margin-right: auto;
}

.profileImg {
    width: 100px;
    height: 100px;
    margin-top: 5px;
    margin-left: auto;
    margin-right: auto;
}

.logBtn {
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

.logBtn:hover {
    color: white;
    border-color: transparent;
    background-color: dodgerblue;
    border-radius: 8px;
}

</style>