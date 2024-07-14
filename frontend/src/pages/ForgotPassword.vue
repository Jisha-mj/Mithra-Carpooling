<template>
  <div style="background-color: #fad3a5; display: flex; flex-direction: column; height: 100vh;">
    <header style="padding: 20px; background-color: white; display: flex; justify-content: space-between; align-items: center;">
      <h1 style="color:#fb0f72;">Mithra Carpooling</h1>
      <div class="header-links">
      <p style="cursor: pointer;margin-right: 20px;" @click="aboutUs"><u>About Us</u></p>
      <p style="cursor: pointer; margin-right: 20px;" @click="signOut"><u>Sign Out</u></p>
      <p style="cursor: pointer;" @click="goToMyProfile"><u>My Profile</u></p>
    </div>
    </header>
    <div style="width: 400px; height: 400px; margin-left:450px; margin-top:100px;">
      <div style="text-align: left; padding: 20px; background-color: rgba(255, 255, 255, 0.75); border-radius: 10px;">
        <h1 style="margin-bottom: 20px; text-align:center">Forget Password</h1>
        <div style="margin-bottom: 10px;">
          <label style="font-weight:bold; margin-right: 85px; text-align:left">Email:</label>
          <input type="email" v-model="email" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; background-color: #FBAF56; width:200px;">
        </div>
        <div style="margin-bottom: 10px;">
          <label style="font-weight:bold; margin-right: 25px; text-align:left">New Password:</label>
          <input type="password" v-model="password" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; background-color: #FBAF56; width:200px;">
        </div>
        <div style="margin-bottom: 20px;">
          <label style="font-weight:bold; margin-right: 10px; text-align:left">Retype Password:</label>
          <input type="password" v-model="retypePassword" required style="text-align:center; border-radius: 10px; border-color: rgba(255, 255, 255, 0.5); height: 30px; background-color: #FBAF56; width:200px;">
        </div>
        <button @click="resetPassword" style="border-radius: 20px; width: 200px; height: 40px; background-color: #FBAF56; font-weight: bold; border-color: white;">Submit</button>
        <p v-if="errorMessage" style="color: red;">{{ errorMessage }}</p>
        <p v-if="noerrorMessage" style="color: green;">{{ noerrorMessage }}</p>
      </div>
    </div>
  </div>
  <footer class="footerComponent" style="margin-top: auto;">
    <p>&copy; 2024 Mithra Carpooling. All rights reserved.</p>
  </footer>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      email: '',
      password: '',
      retypePassword: '',
      errorMessage: '',
      noerrorMessage: ''
    };
  },
  methods: {
    resetPassword() {
      // Basic form validation
      if (!this.email || !this.password || !this.retypePassword) {
        this.errorMessage = 'All fields are required.';
        return;
      }
      if (this.password !== this.retypePassword) {
        this.errorMessage = 'Passwords do not match.';
        return;
      }

      // Reset password logic
      axios.post('http://127.0.0.1:8000/forgot-password/', {
        email: this.email,
        password: this.password,
        re_password: this.retypePassword
      })
      .then(response => {
        this.errorMessage = "";
        console.log(response.data);
        this.noerrorMessage = "Password changed";
        this.email = ''; // Clear email field
        this.password = ''; // Clear password field
        this.retypePassword = ''; // Clear retype password field
        this.$router.push({ name: 'LoginPage' });
      })
      .catch(error => {
        // Handle error
        console.error('Error resetting password:', error);
        this.errorMessage = 'Invalid email id.';
      });
    },
    aboutUs() {
        this.$router.push({ name: 'AboutUs' });
      }
  }
};
</script>

<style>
  /* Add your CSS styles here */
</style>

