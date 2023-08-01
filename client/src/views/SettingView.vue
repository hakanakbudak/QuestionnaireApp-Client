<template>
  <div class="row">

    <div class="col-sm-3">
      <div>
        <SideBar />
      </div>
    </div>

    <div class="col-sm-6">

      <div class="register-view-body">
        <h1>Setting</h1>
        <form>
          <table>
            <tr>
              <td>
                <div class="form-outline-Register">
                  <p>Email Addres</p>
                  <input type="email" v-model="form.email" id="form3Example3" placeholder="Enter a valid email address" />
                </div>
              </td>
              <td>
                <div class="form-outline-Register">
                  <p>Education</p>
                  <input type="text" v-model="form.userEducation" id="form3Example4" placeholder="Education" />
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <div class="form-outline-Register">
                  <p>Username</p>
                  <input type="text" v-model="form.username" id="form3Example3" placeholder="Enter a valid username" />
                </div>
              </td>
              <td>
                <div class="form-outline-Register">
                  <p>Job</p>
                  <input type="text" v-model="form.userJob" id="form3Example3" placeholder=" Job" />
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <div class="form-outline-Register">
                  <p>Password</p>
                  <input type="password" v-model="form.password" id="form3Example4" placeholder="Enter password" />
                </div>
              </td>
              <td>
                <div class="form-outline-Register">
                  <p>City</p>
                  <input type="text" v-model="form.userCity" id="form3Example4" placeholder="City" />
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <div class="form-outline-Register">
                  <p>Brith Date</p>
                  <input type="date" v-model="form.userBirthDate" id="form3Example3" />
                </div>
              </td>
              <td>
                
              </td>
            </tr>
            <tr>
              <td>
                <div class="text-center text-lg-start mt-4 pt-2">
                  <button type="button" @click="updateUserSetting()" class="register-button">Settings save </button>
                </div>
              </td>
            </tr>
          </table>
        </form>
      </div>
    </div>
    <div class="col-sm-3">
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
    SideBar
  },
  data() {
    return {
      form: {
        email: "",
        username: "",
        password: "",
        userBirthDate: "",
        userJob: "",
        userCity: "",
        userEducation: "",
      },
    };
  },

  created() {
    this.getUserSettings();
  },
  methods: {
    async getUserSettings() {
      try {
        const token = localStorage.getItem("access_token");
        const decodedToken = jwt_decode(token);
        const id = decodedToken._id;

        const response = await axios.get(`http://localhost:3000/setting/${id}`, {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        });
        this.form = response.data

        console.log(id)
        console.log(response.data);
      } catch (error) {
        console.error(error);
      }
    },

    updateUserSetting() {
      try {
        const token = localStorage.getItem("access_token");
        const decodedToken = jwt_decode(token);
        const id = decodedToken._id;

        const { email, username, password, userBirthDate, userJob, userCity, userEducation } = this.form;
        const data = {
          email,
          username,
          password,
          userBirthDate,
          userJob,
          userCity,
          userEducation
        };

        const response = axios.put(`http://localhost:3000/setting/${id}`, data, {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        });

        response.then((res) => {
          this.form = res.data; 
        });
      } catch (error) {
        console.log(error);
      }
    },
  }
};
</script>

<style>
.register-view-body {
  width: 700px;
  height: 580px;
  background-color: rgb(241, 138, 12);
  border-radius: 30px;
  border-color: black;
  margin-top: 150px;
  margin-bottom: 20px;
  position: relative;
  margin: auto;
  line-height: 1px;
  background-color: transparent;
}

input {
  height: 40px;
  width: 220px;
  border-radius: 4px;
  border-color: white;
  margin-left: 100px;
}

h1 {
  margin-top: 60px;
  text-align: center;
  ;
  color: white;
}

p {
  color: white;
  text-align: center;
}

a {
  color: white;

}

.login-link-text {
  margin-left: 100px;
}

a:hover {
  color: white;
}



.register-button {
  margin-top: 20px;
  height: 50px;
  width: 220px;
  color: white;
  outline: 0;
  border-radius: 6px;
  border: 2px solid currentcolor;
  border-color: dodgerblue;
  transition: 0.3s ease all;
  background-color: darkblue;
  margin-left: 90px;
}

.register-button:hover {
  color: black;
  background-color: whitesmoke;
  border-radius: 8px;
}

.ımage-upload-button {
  margin-top: 20px;
  height: 50px;
  width: 220px;
  color: white;
  outline: 0;
  border-radius: 6px;
  border: 2px solid currentcolor;
  border-color: dodgerblue;
  transition: 0.3s ease all;
  background-color: darkblue;
  margin-left: 90px;
}

.ımage-upload-button:hover {
  color: black;
  background-color: whitesmoke;
  border-radius: 8px;
}

.form-outline-Register {
  margin-top: 25px;

  font-size: 15px;
  color: aliceblue;
}

.select-profile-photo {
  height: 40px;
  width: 220px;
  border-radius: 4px;
  border-color: white;
  margin-left: 100px;
}
</style>
  
