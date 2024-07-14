<template>
  <div id="SignUpPage" style="background-color:  #fad3a5; display: flex; flex-direction: column; height: 130vh;">
    <header style="padding: 20px; background-color: white; display: flex; justify-content: space-between; align-items: center;">
      <h1 style="margin: 0;color:#fb0f72;">Mithra Carpooling</h1>
      <p style="cursor: pointer;" @click="aboutUs"><u>About Us</u></p>
    </header>
    <p></p>
    <h1 style="text-align:center;">SIGN UP</h1>
    <div class="container" style="flex-grow: 1; display: flex; justify-content: center; align-items: center;">
      <div class="form-container" style="padding: 20px; background-color: rgba(255, 255, 255, 0.5); border: 1px solid black; border-radius: 10px;  max-width: 600px; height:500px;">
        <form @submit.prevent="submit" style="width: 100%;">
          <div style="margin-bottom: 20px;">
            <label for="name" style="font-weight:bold;">Name:</label>
            <input type="text" id="name" v-model="signup.name" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 90px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="email" style="font-weight:bold;">Email:</label>
            <input type="email" id="email" v-model="signup.email" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 90px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="password" style="font-weight:bold;">Password:</label>
            <input type="password" id="password" v-model="signup.password" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 60px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="retypePassword" style="font-weight:bold;">Retype Password:</label>
            <input type="password" id="retypePassword" v-model="signup.retypePassword" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 10px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="age" style="font-weight:bold;">Age:</label>
            <input type="number" id="age" v-model="signup.age" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 100px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="city" style="font-weight:bold;">City:</label>
            <input type="text" id="city" v-model="signup.city" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 100px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="occupation" style="font-weight:bold;">Occupation:</label>
            <input type="text" id="occupation" v-model="signup.occupation" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 50px; background-color: #FBAF56; width:200px;">
          </div>
          <div style="margin-bottom: 20px;">
            <label for="phoneNumber" style="font-weight:bold;">Phone Number:</label>
            <input type="tel" id="phoneNumber" v-model="signup.phoneNumber" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; margin-left: 30px; background-color: #FBAF56; width:200px;">
          </div>
          <button type="submit" style="border-radius: 20px; width: 400px; height: 40px; background-color: #FBAF56; font-weight: bold; border-color: white;">Sign Up</button>
        </form>
        <p v-if="signup.message" style="color: green; text-align: center; margin-top: 20px;">{{ signup.message }}</p>
        <p v-if="signup.errormessage" style="color: red; text-align: center; margin-top: 20px;">{{ signup.errormessage }}</p>
      </div>
    </div>
    <p></p>
    <footer class="footerComponent">
      <p>&copy; 2024 Mithra Carpooling. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SignUpPage",
  data() {
    return {
      signup: {
        name: "",
        email: "",
        password: "",
        retypePassword: "",
        age: "",
        city: "",
        occupation: "",
        phone_number: "",
        message: "",
        errormessage: "",
      }
    };
  },
  methods: {
    submit() {
      axios.post("http://127.0.0.1:8000/Signup/", this.signup)
        .then(response => {
          console.log(response.data);
          if (response.data.message === "signup successful") {
            console.log(response.data.uid)
            this.$router.push({ name: "IDproofUploadPage", params: { uid: response.data.uid } });
          } else {
            this.signup.errormessage = response.data.message;
          }
        })
        .catch(error => {
          console.error(error);
          this.signup.errormessage = "An error occurred during signup.";
        });
    },
    aboutUs() {
      this.$router.push({ name: "AboutUs" });
    }
  }
};
</script>

<style>
#SignUpPage {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.container {
  flex-grow: 1;
}

.form-container {
  padding: 20px;
  border: 1px solid black;
  border-radius: 10px
}

button {
  display: block;
  margin: 0 auto;
}
.footerComponent {
  background: linear-gradient(90deg, #fb0f72, #f9a84a);
  padding: 20px;
  text-align: center;
  color: white;
}
.footerComponent {
  background: linear-gradient(90deg, #fb0f72, #f9a84a);
  padding: 20px;
  text-align: center;
  color: white;
}
</style>
