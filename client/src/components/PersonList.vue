<template>
    <div>
        <!--

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
                        </table>
                        
                        
                    </div>
                </div>
            </div>
        </div>
    -->

        <SideBar />

        <div class="row">
            <div class="col-sm-3"></div>

            <div class="col-sm-5">

                <div class="searchDiv">
                    <input class="searchBar" type="search" placeholder="Search...">
                </div><br>
                <br>

                <div v-for="person in persons" :key="person._id" class="card my-4">

                    <div class="card">
                        <div class="card-body">


                            <ul class="list-group list-group-vertical">
                                <h5 class="card-title">{{ person.category }}</h5>
                                <li class="list-group-item">{{ person.age }}</li> <button type="button">%555</button>
                                <li class="list-group-item">{{ person.country }}</li><button type="button">%555</button>
                                <li class="list-group-item">{{ person.city }} </li><button type="button">%555</button>
                                <li class="list-group-item">{{ person.message }} </li><button type="button">%555</button>
                            </ul>

                            <br>

                            <button type="button" @click="editPerson(person._id)" class="btn btn-primary"> Edit </button>
                            <button type="button" @click="removePerson(person._id)" class="btn text-white "
                                style="background-color: red;">Delete</button>

                        </div>

                    </div>

                </div>

            </div>
            <div class="col-sm-3"></div>

        </div>



    </div>
</template>
<script>

import router from "../router";
import axios from "axios";
import SideBar from "../components/SideBar.vue"

export default {

    components: {
        SideBar
    },

    data() {
        return {
            persons: []
        }
    },

    created() {
        this.getPersons()
    },

    methods: {
        async getPersons() {
            try {
                const response = await axios.get('http://localhost:3000/persons')
                this.persons = response.data


            } catch (error) {
                console.error(error)
            }
        },


        async removePerson(_id) {
            try {
                await axios.delete(`http://localhost:3000/persons/${_id}`);
                this.getPersons();
            } catch (error) {
                console.log(error);
            }
        },

        editPerson(_id, age, country, city) {
            try {
                const response = axios.put(`http://localhost:3000/update/${_id}`, { age, country, city })
                this.response = response.data,

                    console.log(response),
                    router.replace({
                        path: `/update/${_id}`,
                    });

            }
            catch (error) {
                console.log(error)
            }
        },

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

    },


};

</script>

<style>
.searchBar {
    width: auto;
    height: auto;
    border-radius: 10px;
    border-color: black;
    text-align: center;
    margin-left: 10px;
    margin-top: 6px;
}

.searchDiv {
    margin-bottom: 0;
    width: 615px;
    height: 50px;
    background-color: rgba(0, 0, 139, 0.137);
    z-index: 1;
    border-radius: 10px;
}
</style>

