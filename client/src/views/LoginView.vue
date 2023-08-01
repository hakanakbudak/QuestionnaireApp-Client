<template >
  <div class="row">
    <div class="col-sm-3"></div>
    <div class="col-sm-6">
      <div class="login-view-body">
        <form>
          <h1 class="login-text">Login</h1><br>
          <tr>
            <div class="form-outline-Login">
              <p class="p-text">Email Addres</p>
              <input type="email" v-model="form.email" id="form3Example3" placeholder="Enter a valid email address" />
              <p class="p-text">Password</p>
              <input type="password" v-model="form.password" id="form3Example4" placeholder="Enter password" />

            </div>
          </tr>
          <tr>
            <button type="button" @click="userLogin()" class="login-button"
              style="padding-left: 2.5rem; padding-right: 2.5rem;">Login</button>
            <div>
              <p class="register-link">Don't have an account?
                <button @click="goToRegisterPage()" class="link-danger">Register</button>
              </p>
            </div>
          </tr>
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
        password: "",
      },
      isSnackBarShown: false,
    };
  },
  methods: {
    userLogin() {
      axios
        .post("http://localhost:3000/login", this.form, {
          headers: {
            "Access-Control-Allow-Origin": "http://localhost:3000/login",
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          withCredentials: false,
        })
        .then(
          (response) => {
            if (response.data) {
              localStorage.access_token = response.data;
              router.push({
                path: "/questionnaire",
              });
            }
          },
          (error) => {
            console.log(error);
          }
        );
    },
    goToRegisterPage(){
      router.push({
        path:"/register"
      })
    }
  },
};
</script>

<style>
input {
  height: 40px;
  width: 220px;
  border-radius: 4px;
  border-color: white;
}

h1 {
  margin-top: 80px;
  line-height: 100px;
  margin-left: 140px;
  color: white;
}

.link-danger{
  background-color: transparent;
  border-color: transparent;
}

.login-view-body {
  background-color: transparent;
  border-radius: 5px;
  margin: auto;
  width: 400px;
  height: 450px;
}

.login-button {
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
  margin-left: 100px;
}

.login-button:hover {
  color: black;
  background-color: whitesmoke;
  border-radius: 8px;
}

.form-outline-Login {
  text-align: center;
  margin-left: 90px;
}

.register-link {
  text-align: center;
  margin-left: 90px;
  color: white;
}

.p-text {
  color: white;
}

.link-danger {
  color: white;
}

.login-text{
  margin-left: 125px;
  font-size: 70px;
}
</style>