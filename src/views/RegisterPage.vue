<template>
  <div class="wrapper"> <!-- Added wrapper class here -->
    <!-- Header with Logo and Login Link -->
    <header class="header">
      <div class="container">
        <!-- Left side with logo -->
        <div class="logo">
          <img src="@/assets/vihologo.png" alt="Logo">
        </div>

        <!-- Right side with login link -->
        <div class="login">
          <router-link to="/" class="login-link">Already a partner?</router-link>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="main-content">
      <!-- Left-side content with sliding text -->
      <div class="left-side">
        <p class="sliding-text">
          List your <br>
          <span id="sliding-part">{{ currentText }}</span> <br>
          on Vihobook.com
        </p>
      </div>

      <!-- Right-side content with card -->
      <div class="right-side">
        <div class="card">
          <form @submit.prevent="handleRegister">
            <h2>Register</h2>
            <div class="form-group">
              <label for="membershipCode">Membership Code</label>
              <input type="text" id="membershipCode" v-model="membershipCode" required>
            </div>
            <div class="form-group">
              <label for="email">Email</label>
              <input type="email" id="email" v-model="email" required>
            </div>
            <div class="form-group">
              <label for="password">Password</label>
              <input type="password" id="password" v-model="password" required>
            </div>
            <button type="submit" class="btn">Register</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';

export default defineComponent({
  name: 'RegisterPage',
  setup() {
    const slidingText = ['home', 'bungalow', 'hotel', 'villa', 'anything'];
    const index = ref(0);
    const currentText = ref(slidingText[index.value]);

    const membershipCode = ref('');
    const email = ref('');
    const password = ref('');

    const changeText = () => {
      index.value = (index.value + 1) % slidingText.length;
      currentText.value = slidingText[index.value];
    };

    const handleRegister = () => {
      // Handle registration logic here
      console.log('Registration details:', {
        membershipCode: membershipCode.value,
        email: email.value,
        password: password.value,
      });
    };

    onMounted(() => {
      setInterval(changeText, 2000); // Change text every 2 seconds
    });

    return {
      currentText,
      membershipCode,
      email,
      password,
      handleRegister,
    };
  },
});
</script>

<style scoped>
/* Global Styles */
html, body {
    height: 100%;
    margin: 0;
    padding: 0;
    overflow: hidden; /* Optional: prevent scrolling */
}

.wrapper {
    display: flex;
    flex-direction: column; /* Arrange children vertically */
    height: 100vh; /* Full viewport height */
    width: 100vw; /* Full viewport width */
}

/* CSS for header */
.header {
  background-color: #f0f0f0;
  padding: 20px 0;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  width: 70%;
  margin: 0 auto;
}

.logo img {
  height: 50px;
  width: auto;
}

.login-link {
  text-decoration: none;
  color: #333;
  margin-right: 20px;
}

.login-link:hover {
  text-decoration: underline;
}

/* CSS for main content */
.main-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex: 1; /* Ensure it takes available space */
  padding: 20px;
}

.left-side {
  width: 60%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.sliding-text {
  font-size: 24px;
  font-weight: bold;
  line-height: 1.5;
}

#sliding-part {
  color: blue;
  display: inline-block;
  margin: 10px 0;
}

.right-side {
  width: 35%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-right: 90px;
}

.card {
  background-color: #fff;
  padding: 60px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  width: 100%;
  text-align: center;
  margin-right: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.btn {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn:hover {
  background-color: #0056b3;
}
</style>
