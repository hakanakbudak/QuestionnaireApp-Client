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
                <div class="text-center text-lg-start mt-4 pt-2">
                  <button type="button" @click="register" class="register-button"
                    style="padding-left: 2.5rem; padding-right: 2.5rem;">Register</button>
                  <div class="login-link-text">
                    <p class="small fw-bold mt-2 pt-1 mb-0">Don't have an account?
                      <a href="http://localhost:8080/login" class="link-danger">Login</a>
                    </p>
                  </div>
                </div>
              </td>

              <td>
                <div class="form-outline-Register">
                  <p>Brith Date</p>
                  <input class="input-date" type="date" v-model="form.userBirthDate" id="form3Example3" />
                </div>
              </td>
            </tr>

          </table>

        </form>

      </div>
    </div>

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
        userBirthDate: "",
        userJob: "",
        userCity: "",
        userEducation: "",
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
  margin-top: 60px;
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

.login-link-text {
  margin-left: 100px;
}

a:hover {
  color: white;
}

.register-button {
  color: white;
  outline: 0;
  border: 2px solid currentcolor;
  border-color: dodgerblue;
  transition: 0.3s ease all;
  background-color: dodgerblue;
  font-size: 15px;
  font-weight: 600;
  padding: 20px 15px;
  margin-left: 100px;
  display: inline-block;
}

.register-button:hover {
  color: black;
  border-color: transparent;
  background-color: white;
  border-radius: 8px;
}

.form-outline-Register {
  margin-top: 25px;
  line-height: 1px;
  font-size: 15px;
  font-weight: 600;
  color: aliceblue;
}

.register-view-body {
  width: 700px;
  height: 480px;
  background-color: rgb(241, 138, 12);
  border-radius: 30px;
  border-color: black;
  margin-top: 150px;
  margin-bottom: 20px;
  position: relative;
  margin: auto;
  line-height: 1px;
  background: linear-gradient(90deg, rgba(2, 0, 36, 1) 0%, rgba(9, 9, 121, 1) 35%, rgba(0, 212, 255, 1) 100%);
}

.input-date {
  width: 190px;
  height: 50px;
}
</style>
  
