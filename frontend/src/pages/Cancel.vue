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
    <h1 style="text-align: center;">CANCELLATION</h1>
    <!-- Display Available Carpools -->
    <div v-if="availableCarpools.length" style="background-color: #fad3a5;">
      <h3>CANCEL JOINED CARPOOL</h3>
      <div v-for="carpool in availableCarpools" :key="carpool.id" class="carpool-box">
        <div class="user-details">
          <p><strong>Driver Name:</strong> {{ carpool.driverName }}</p>
          <p><strong>Route: </strong>{{ carpool.route }}</p>
          <p><strong>Start: </strong>{{ carpool.start }}</p>
          <p><strong>End: </strong>{{ carpool.end }}</p>
          <p><strong>Date: </strong>{{ carpool.date }}</p>
          <p><strong>Start </strong>Time: {{ carpool.time }}</p>
          <p><strong>Status: </strong>{{ carpool.status }}</p>
          <p><strong>Price: </strong>{{ carpool.price }}</p>
          <!-- Link to view driver's profile -->
          <a href="#" class="profile-link" @click="viewProfile(carpool)">View profile</a>
        </div>
        <div class="button">
          <button class="cancel-button" @click="cancel(carpool)">Cancel</button>
        </div>
      </div>
    </div>
    <!-- Display Available Carpools -->
    <div v-if="availableDelivery.length" style="background-color: #fad3a5;">
      <h3>CANCEL PRODUCT DELIVERY</h3>
      <div v-for="carpool in availableDelivery" :key="carpool.id" class="carpool-box">
        <div class="user-details">
          <p><strong>Driver Name: </strong>{{ carpool.driverName }}</p>
          <p><strong>Route: </strong>{{ carpool.route }}</p>
          <p><strong>Start: </strong>{{ carpool.start }}</p>
          <p><strong>End: </strong>{{ carpool.end }}</p>
          <p><strong>Date: </strong>{{ carpool.date }}</p>
          <p><strong>Start Time: </strong>{{ carpool.time }}</p>
          <p><strong>Product weight: </strong>{{ carpool.wgt }}</p>
          <p><strong>Product size: </strong>{{ carpool.size }}</p>
          <p><strong>Product type: </strong>{{ carpool.type }}</p>
          <div v-if="carpool.anyother">
            <p><strong>Product weight: </strong>{{ carpool.anyother }}</p>
          </div>
          <p><strong>Status: </strong>{{ carpool.status }}</p>
          <p><strong>Price: </strong>{{ carpool.price }}</p>
          <!-- Link to view driver's profile -->
          <a href="#" class="profile-link" @click="viewProfile(carpool)">View profile</a>
        </div>
        <div class="button">
          <button class="cancel-button"@click="cancel(carpool)">Cancel</button>
        </div>
      </div>
    </div>
    <div v-if="CreatedCarpool.length" style="background-color: #fad3a5;">
      <h3>CANCEL CREATED CARPOOL</h3>
      <div v-for="carpool in CreatedCarpool" :key="carpool.id" class="carpool-box"> 
        <div class="user-details" style="">
          <p><strong>Route:</strong> {{ carpool.route }}</p>
          <p><strong>Start:</strong> {{ carpool.start }}</p>
          <p><strong>End:</strong> {{ carpool.end }}</p>
          <p><strong>Date:</strong> {{ carpool.date }}</p>
          <p><strong>Start Time:</strong> {{ carpool.time }}</p>
          <p><strong>Price:</strong> {{ carpool.price }}</p>
        </div>
        <div class="button">
          <button class="cancel-button" @click="cancel(carpool)">Cancel</button>
        </div>
      </div>
    </div>
    <p v-if="this.errormessage" style="color: red;">{{ this.errormessage }}</p>
  </div>
  <footer class="footerComponent">
      <p>&copy; 2024 Mithra Carpooling. All rights reserved.</p>
    </footer>
</template>

<script>
import axios from 'axios';

export default {
  props: ['driverParams'],
  data() {
    return {
      availableDelivery: [],
      availableCarpools: [],
      CreatedCarpool: [],
      errormessage: "",
    };
  },
  mounted(){
    this.searchCarpools();
    this.searchCreatedCarpool();
    this.searchProduct();
  },
  methods: {
    searchCarpools() {
      axios.post('http://127.0.0.1:8000/cancel-content/')
      .then(({data}) => {
    console.log("Received data from backend:", data);
    if (Array.isArray(data)) {
      this.availableCarpools = data;
    } else {
      this.errormessage = data.message; // Display error message if no rides are available
    }
  })
  .catch(error => {
    console.error('Error fetching carpools:', error);
    this.errormessage = "Error fetching carpools";
  });
    },
    searchProduct() {
      axios.get('http://127.0.0.1:8000/cancel-content/')
      .then(({data}) => {
    console.log("Received data from backend:", data);
    if (Array.isArray(data)) {
      this.availableDelivery = data;
    } else {
      this.errormessage = data.message; // Display error message if no rides are available
    }
  })
  .catch(error => {
    console.error('Error fetching carpools:', error);
    this.errormessage = "Error fetching carpools";
  });
    },
    cancel(carpool)
    {
      axios.post('http://127.0.0.1:8000/cancel/', carpool)
      .then(response => {
          console.log(response.data);
          this.availableCarpools=[];
          this.availableDelivery=[];
          this.CreatedCarpool=[];
          this.searchProduct();
          this.searchCarpools();
          this.searchCreatedCarpool();
        })
        .catch(error => {
          console.error('Error requesting carpool:', error);
          this.errormessage = "Error requesting product delivery";
        });
    },
    searchCreatedCarpool() {
      axios.put('http://127.0.0.1:8000/cancel-content/')
      .then(({data}) => {
    console.log("Received data from backend:", data);
    if (Array.isArray(data)) {
      this.CreatedCarpool = data;
    } else {
      this.errormessage = data.message; 
    }
  })
  .catch(error => {
    console.error('Error fetching carpools:', error);
    this.errormessage = "Error fetching carpools";
  });
    },
    viewProfile(carpool) {
        axios.post('http://127.0.0.1:8000/driver-id-save/', {driver_id: carpool.id})
        .then(response => {
          console.log(response.data);
          this.$router.push({ name: "ViewProfile" });
        })
        .catch(error => {
          console.error('Error viewing profile:', error);
          this.errormessage = "Error viewing profile";
        });
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
    .profile-link {
        color: blue;
        text-decoration: underline;
    }

    .cancel-button{
      background-color: lightpink;
      color: black;
      margin-right: 10px;
    }

    .user-box {
      background-color: white;
      margin-bottom: 20px;
      margin-left:30px;
      display: flex;
      justify-content: space-between;
      padding: 20px;
      width: 1100px;
    }

    .button{
      display: flex;
    }
</style>