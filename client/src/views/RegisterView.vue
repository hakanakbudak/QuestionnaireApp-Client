<template>
  <section class="vh-100">
    <div class="container-fluid h-custom">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-md-9 col-lg-6 col-xl-5"><br>
          <h1 class="text-black">REGISTER</h1><br>
          <img src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.webp" class="img-fluid"
            alt="Sample image"><br>
        </div>
        <div class="col-md-8 col-lg-6 col-xl-4 offset-xl-1"><br>
          <form>
            <div class="d-flex flex-row align-items-center justify-content-center justify-content-lg-start">
              <p class="lead fw-normal mb-0 me-3">Register in with</p>
              <button type="button" class="btn btn-primary btn-floating mx-1">
                <i class="fab fa-facebook-f">facebook</i>
              </button>

              <button type="button" class="btn btn-primary btn-floating mx-1">
                <i class="fab fa-twitter">twitter</i>
              </button>

              <button type="button" class="btn btn-primary btn-floating mx-1">
                <i class="fab fa-linkedin-in">linkedin</i>
              </button>
              <p class="text-center fw-bold mx-3 mb-0">Or</p>
            </div><br>

            <!-- Email input -->
            <div class="form-outline mb-4">
              <label class="form-label" for="form3Example3">Email address</label>
              <input type="email" v-model="form.email" id="form3Example3" class="form-control form-control-lg"
                placeholder="Enter a valid email address" />
            </div>

            <!-- User input -->
            <div class="form-outline mb-4">
              <label class="form-label" for="form3Example3">Username</label>
              <input type="text" v-model="form.username" id="form3Example3" class="form-control form-control-lg"
                placeholder="Enter a valid username" />
            </div>

            <!-- Password input -->
            <div class="form-outline mb-3">
              <label class="form-label " for="form3Example4">Password</label>
              <input type="password" v-model="form.password" id="form3Example4" class="form-control form-control-lg"
                placeholder="Enter password" />
            </div>

            <div class="d-flex justify-content-between align-items-center">
              <!-- Checkbox -->
              <div class="form-check mb-0">
                <input class="form-check-input me-2" type="checkbox" value="" id="form2Example3" />
                <label class="form-check-label " for="form2Example3">Remember me </label>
              </div>
              <a href="#!" class="text-body">Forgot password?</a>
            </div>

            <div class="text-center text-lg-start mt-4 pt-2">
              <button @click="register" type="button" class="btn btn-primary btn-lg"
                style="padding-left: 2.5rem; padding-right: 2.5rem;">Register</button>
              <p class="small fw-bold mt-2 pt-1 mb-0">I have a account ! <a href="http://localhost:8080/login"
                  class="link-danger">Login</a>
              </p>
            </div>

          </form>
        </div><br>
      </div><br>
    </div><br>
    <div
      class="d-flex flex-column flex-md-row text-center text-md-start justify-content-between py-4 px-4 px-xl-5 bg-primary">
      <!-- Copyright -->
      <div class="text-white mb-3 mb-md-0"><br>
        Copyright © 2020. All rights reserved.
      </div>
      <!-- Copyright -->

      <!-- Right -->

      <!-- Right -->
    </div>
  </section>
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


        )
      return {
        
        
      }
    },



  },
};
</script>
  
