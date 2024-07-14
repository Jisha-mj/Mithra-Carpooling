<template>
  <div id="SignUpPage" style="background-color:  #fad3a5; display: flex; flex-direction: column; height: 150vh;">
    <header style="padding: 20px; background-color: white; display: flex; justify-content: space-between; align-items: center;">
      <h1 style="color:#fb0f72;">Mithra Carpooling</h1>
      <div class="header-links">
        <p style="cursor: pointer;margin-right: 20px;" @click="aboutUs"><u>About Us</u></p>
        <p style="cursor: pointer; margin-right: 20px;" @click="signOut"><u>Sign Out</u></p>
        <p style="cursor: pointer;" @click="goToMyProfile"><u>My Profile</u></p>
      </div>
    </header>
  <div class="payment-container">
    <h1 class="payment">PAYMENT</h1>
    <!-- Main picture in the middle -->
    <img :src="mainPicture" alt="Main Picture" class="main-picture">
    
    <!-- Four small pictures at the bottom -->
    <div class="small-pictures">
      <img v-for="(link, index) in smallPictures" :src="link" :key="index" @click="redirectToWebsite(index)" class="small-picture" style="cursor: pointer;">
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      mainPicture: '', // Path to the main picture passed by Django
      smallPictures: [ // Paths to the small pictures
        '/rectangle-55@2x.png',
        '/rectangle-53@2x.png',
        '/rectangle-54@2x.png',
        '/rectangle-52@2x.png'
      ],
      websites: [ // Corresponding websites for small pictures
        'https://udyogini.org/',
        'https://dashboard.kerala.gov.in/e-services/service.php?fcgzGljlql',
        'https://wcd.nic.in/bbbp-schemes',
        'https://web.umang.gov.in/landing/department/pmmvy.html'
      ]
    };
  },
  mounted() {
    axios.get('http://127.0.0.1:8000/final-payment/')
    .then(response => {
      this.mainPicture = response.data.mainPicture;
    })
    .catch(error => {
      console.error('Error fetching main picture:', error);
    });
},
  methods: {
    redirectToWebsite(index) {
      window.open(this.websites[index], '_blank');
    },
    aboutUs() {
      this.$router.push({ name: "AboutUs" });
    },
    signOut() {
      this.$router.push({ name: "StPage" });
    },
    goToMyProfile() {
      this.$router.push({ name: "YourProfile" });
    }
  }
};
</script>

<style>
.payment-container {
  --color-navajowhite: #fad3a5;
  background-color: var(--color-navajowhite);
  padding: 20px;
}

.payment {
  text-align: center;
  font-size: 40px;
}
.main-picture {
  display: block;
  margin: 0 auto;
  width: 400px;
}

.small-pictures {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.small-picture {
  width: 250px;
  height: 200px;
  margin: 0 10px;
}
</style>
