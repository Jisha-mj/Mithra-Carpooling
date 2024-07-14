<template>
  <div id="AboutUs" style="background-color: #fad3a5; display: flex; flex-direction: column; height: 88vh;">
    <header style="padding: 20px; background-color: white; display: flex; justify-content: space-between; align-items: center;">
      <h1 style="color:#fb0f72;">Mithra Carpooling</h1>
    </header>
    <div class="content">
      <p class="heading">ABOUT US</p>
      <p style="text-align: center; font-family: 'Space Grotesk'; font-size: 20px;">Welcome to Mithra, women’s only carpooling where we introduce a safer platform for women to share rides together.</p>
    <p style="text-align: center; font-family: 'Space Grotesk'; font-size: 20px; margin-bottom: -10px; margin-top: 30px;">Our vision is to build a strong community by connecting women across Kerala. Our services range from ride-sharing</p>
    <p style="text-align: center; font-family: 'Space Grotesk'; font-size: 20px; margin-bottom: -10px;">to product delivery services. What sets us apart is our attention to detail and dedication to quality. We put our hearts and</p>
    <p style="text-align: center; font-family: 'Space Grotesk'; font-size: 20px; margin-bottom: 20px;">souls into whatever we do. Our journey is guided by core values like integrity, innovation, and excellence.</p>
      
      <!-- Additional lines of text and image -->
      <div class="additional-content">
        <div class="paragraph2">
          <p>Meet our expert team</p>
          <p>Teena Vithayathil -Backend Developer</p>
          <p> Jisha Maria Joseph- UI/UX Developer</p>
          <p> Hima Sony-Database Designer</p>
        </div>
        <div class="image-container">
          <img src="/rectangle-39@2x.png" alt="Description of your image" style="width: 500px; height: 250px; border-radius: 20px;">
        </div>
      </div>
    </div>
    <footer class="footerComponent" style="margin-top: 40px;">
      <p>&copy; 2024 Mithra Carpooling. All rights reserved.</p>
    </footer>
  </div>
</template>

<style>
#AboutUs {
  display: flex;
  flex-direction: column;
  height: 88vh;
  background-color: #fad3a5;
}

header {
  padding: 20px;
  background-color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.heading {
  text-align: center;
  font-weight: bold;
  font-size: 30px;
  font-family: 'Irish Grover';
  margin-top: 20px;
}

.paragraph {
  text-align: center;
  font-family: 'Space Grotesk';
  font-size: 20px;
  margin-bottom: 20px;
}

.additional-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-top: 20px;
  font-family: 'Space Grotesk';
}

.paragraph2 {
  flex: 1;
  padding: 0 20px;
  font-family: 'Space Grotesk';
  font-size: 20px;
}

.image-container {
  flex: 1;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-right: 20px;
  margin-bottom: -26px;
}

.image-container img {
  max-width: 100%;
  height: auto;
}
</style>
