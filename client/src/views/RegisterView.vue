<template>
  <div class="row">

    <div class="col-sm-3"></div>

    <div class="col-sm-6">

      <div class="register-view-body">
        <h1>Register</h1>
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
                <div class="form-outline-Register">
                  <p>Select Profile Image</p>
                  <input class="select-profile-photo" type="file" @change="handleFileUpload()" />
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <div class="text-center text-lg-start mt-4 pt-2">
                  <button type="button" @click="register()" class="register-button">Register</button>
                  <div class="login-link-text">
                    <p class="small fw-bold mt-2 pt-1 mb-0">Don't have an account?
                      <button @click="goToLoginpage()" class="link-danger">Login</button>
                    </p>
                  </div>
                </div>
              </td>
              <td>
                <div class="text-center text-lg-start mt-3">
                  <button @click="uploadImage()" class="ımage-upload-button">Resim Yükle</button>
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
export default {
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
        file: null,
      },
    };
  },
  methods: {
    register() {
      axios
        .post("http://localhost:3000/register", this.form, {
          headers: {
            "Access-Control-Allow-Origin": "*",
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          withCredentials: false,
        })
        .then(
          (response) => {
            console.log(response);
            router.replace({
              path: "/login",
            });
          },
          (error) => {
            console.log(error);
          }
        )
    },
    goToLoginpage() {
      router.replace({
        path: "/login",
      });
    },
    handleFileUpload(event) {
      this.file = event.target.files[0];
    },
    uploadFile() {
      const formData = new FormData();
      formData.append('file', this.file);
      axios.post('http://localhost:3000/register', this.form)
        .then((response) => {
          console.log(response.data);
        })
        .catch((error) => {
          console.error(error);
        });
    }
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
  background-color: dodgerblue;
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

.link-danger {
  background-color: transparent;
  border-color: transparent;
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
}</style>
  
