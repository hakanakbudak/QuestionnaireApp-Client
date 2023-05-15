<template>
  <div class="row">

    <div class="col-sm-3"></div>

    <div class="col-sm-6">

      <div class="registerBody">
        <h1>Register</h1>
        <form>
          <!-- Username input -->
          <div class="form-outline-Register">
            <p>Email Addres</p>
            <input type="email" v-model="form.email" id="form3Example3" placeholder="Enter a valid email address" />
          </div>
          <!-- Email input -->
          <div class="form-outline-Register">
            <p>Username</p>
            <input type="email" v-model="form.username" id="form3Example3" placeholder="Enter a valid username" />
          </div>
          <!-- Password input -->
          <div class="form-outline-Register">
            <p>Password</p>
            <input type="password" v-model="form.password" id="form3Example4" placeholder="Enter password" />
          </div>

          <div class="text-center text-lg-start mt-4 pt-2">
            <button type="button" @click="register" class="registerBtn"
              style="padding-left: 2.5rem; padding-right: 2.5rem;">Register</button>
            <p class="small fw-bold mt-2 pt-1 mb-0">Don't have an account? <a href="http://localhost:8080/login"
                class="link-danger">Login</a>
            </p>
          </div>

        </form>

      </div>
    </div>

    <div class="col-sm-3"></div>

  </div>
  
</template>
  
<script>
import axios from "axios";
export default {
  data() {
    return {
      form: {
        email: "",
        username: "",
        password: "",
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
        )},
  },
};
</script>

<style>
body {
  background-color: aliceblue;
}

input {
  border-radius: 10px;
  border-color: white;
  text-decoration: none;
  padding: 8px 4px;
  font-size: 15px;
  font-weight: 400;
  line-height: 1px;
  margin-left: 100px;

}

h1 {
  margin-top: 80px;
  margin-left: 130px;
  line-height: 100px;
  color: white;
}

p {
  color: white;
  text-align: center;
}

a {
  color: white;
}

a:hover {
  color: white;
}

.registerBtn {
  color: white;
  outline: 0;
  border: 2px solid currentcolor;
  border-color: dodgerblue;
  transition: 0.3s ease all;
  background-color: dodgerblue;
  font-size: 15px;
  font-weight: 600;
  padding: 20px 15px;
  display: inline-block;
}

.registerBtn:hover {
  color: black;
  border-color: transparent;
  background-color: white;
  border-radius: 8px;
}

.form-outline-Register {
  margin-top: 45px;
  line-height: 1px;
  font-size: 15px;
  font-weight: 600;
  color: aliceblue;
}

.registerBody {
  background-color: rgb(241, 138, 12);
  border-radius: 30px;
  border-color: black;
  /*padding: 2px 2px;*/
  margin-top: 150px;
  margin-bottom: 20px;
  position: relative;
  margin: auto;
  width: 400px;
  height: 520px;
  line-height: 1px;
  background: linear-gradient(90deg, rgba(2, 0, 36, 1) 0%, rgba(9, 9, 121, 1) 35%, rgba(0, 212, 255, 1) 100%);
}
</style>
  
