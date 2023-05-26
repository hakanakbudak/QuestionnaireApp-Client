<template>
    <div class="row">

        <div class="col-sm-4">
            <SideBar />
        </div>

        <div class="col-sm-4">

            <div class="card">
                <div class="card-body">


                    <form>
                        <table>
                            <tr>
                                <td>
                                    <p>BirtDate</p>
                                    <input type="text">
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <p>Job</p>
                                    <input type="text">
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <p>City</p>
                                    <input type="text">
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <p>Education</p>
                                    <input type="text">
                                </td>
                            </tr>
                            <br>
                            <tr>
                                <td>
                                    <button class="setting-button" type="button">Update</button>
                                </td>
                            </tr>
                        </table>
                    </form>


                </div>

            </div>


        </div>

        <div class="col-sm-4">

        </div>

    </div>
</template>

<script>
import router from "../router";
import SideBar from "../components/SideBar.vue"
import axios from "axios";

export default {

    components: {
        SideBar,
    },

    data() {
        return {
            //persons: []
        }
    },

    methods: {
        async getSetting() {
            try {
                const response = await axios.get('http://localhost:3000/setting')
                this.persons = response.data


            } catch (error) {
                console.error(error)
            }
        },


    }

};
</script>

<style>
.card {
    margin-top: 50px;
}

.setting-button {
  width: 190px;
  color: white;
  outline: 0;
  border: 2px solid currentcolor;
  border-color: dodgerblue;
  transition: 0.3s ease all;
  background-color: dodgerblue;
  padding: 20px 15px;
  display: inline-block;
}

.setting-button:hover {
  color: black;
  border-color: transparent;
  background-color: white;
  border-radius: 8px;
}
</style>