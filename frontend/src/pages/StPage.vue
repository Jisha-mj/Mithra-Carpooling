<template>
  <div id="AboutUs" style="display: flex; flex-direction: column; height: 88vh; position: relative;">
    <header style="padding: 20px; background-color: white; display: flex; justify-content: space-between; align-items: center;">
      <h1 style="color: #fb0f72;">Mithra Carpooling</h1>
      <button style="cursor: pointer; margin-right: 20px; background-color: beige; border-radius: 20px; width: 100px; height: 50px; border-color: white;" @click="about">About Us</button>
    </header>
    <div class="content">
      <!-- Three lines of text on top of the image -->
      <div class="text-lines">
        <h1 style="margin-top: 80px; margin-left: 50px; font-size: 60px; color: #FB0F72;">MITHRA</h1>
        <h1 style="margin-left: 50px; font-size: 40px; margin-top: -20px; color: #FB0F72;">BRIDGING DISTANCES BUILDING BONDS</h1>
        <h1 style="margin-left: 50px; margin-top: -20px; color: #6f0632;">Your most trusted travel companion, women's exclusive carpooling community</h1>
        
        <!-- Button box on top of the image -->
        <div class="button-box">
          <button class="button-login" @click="login">Login</button>
          <button class="button-signup" @click="signup">Sign up</button>
        </div>
      </div>
      
      <!-- Main image with overlay -->
      <div class="main-image" style="position: relative;">
        <img class="child-img" src="/rectangle-1@2x.png" style="height: 522px; width: 1519px; opacity: 0.7;">
        <div class="overlay">
        </div>
      </div>
    </div>
    <footer class="footerComponent">
      <p>&copy; 2024 Mithra Carpooling. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
  import { defineComponent } from "vue";
  export default defineComponent({
    name: "StPage",
    methods: {
      about() {
        this.$router.push({ name: "AboutUs" });
      },
      signup() {
        this.$router.push({ name: "SignupPage" });
      },
      login() {
        this.$router.push({ name: "LoginPage" });
      }
    },
  });
</script>

<style scoped>
/* Additional styling for the template */

.content {
  position: relative; /* Ensure content is positioned relative to the parent */
}

.text-lines {
  position: absolute; /* Position the text lines absolutely */
  top: 20px; /* Adjust top position as needed */
  left: 20px; /* Adjust left position as needed */
  padding: 10px;
  border-radius: 8px;
  z-index: 1; /* Ensure text is above the image */
}

.button-box {
  position: absolute;
  top: 350px;
  left: 350px;
  border-radius: 200px;
  width: 350px;
  height: 80px;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.9); /* White background with transparency */
  padding: 20px;
  border-radius: 8px;
}

.button-login,
.button-signup {
  padding: 10px 20px;
  background-color: #dd5d02;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 20px;
  font-size: 16px;
  width: 120px;
}

.button-login:hover,
.button-signup:hover {
  background-color: #ff3f9e;
}

.main-image {
  position: relative;
}

.child-img {
  height: 522px;
  width: 1519px;
  opacity: 0.7;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(180, 179, 176, 0.449); /* Semi-transparent black background */
}
</style>
