<template>
  <div class="wrapper">
    <div class="left-section">
      <div class="left-content">
        <h1>Welcome to the<br> Vihobook <br>Extranet!</h1>
        <p class="dont-have-account">Don't have an account?</p>
        <router-link to="/register" class="signup-button">Sign Up</router-link>
      </div>
    </div>
    <div class="right-section">
      <div class="login-container">
        <img src="@/assets/vihologo.png" alt="Logo" class="logo" />
        <form @submit.prevent="handleSubmit">
          <input v-model="membershipCode" type="text" placeholder="Membership Code" required />
          <input v-model="email" type="email" placeholder="Email" required />
          <input v-model="password" type="password" placeholder="Password" required />
          <div class="remember-forgot-container">
            <label for="checkbox" class="checkbox d-flex align-items-center text-base cursor-pointer text-gray">
              <input id="checkbox" type="checkbox" v-model="rememberMe" class="checkbox mr-1" />Remember me
            </label>
            <a href="#" class="forgot-password">Forgot Password?</a>
          </div>
          <router-link to="/dashboard" class="login-button">
            <button type="button">Login</button>
          </router-link>
          <p class="terms-text">
            By signing in or creating an account, you agree with our
            <a href="#" @click.prevent="openModal">Terms & Conditions</a> and
            <a href="#">Privacy Statement</a>.
          </p>
        </form>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'LoginPage',
  setup() {
    // Data fields
    const membershipCode = ref('');
    const email = ref('');
    const password = ref('');
    const rememberMe = ref(false);
    const showModal = ref(false);

    // Methods
    const handleSubmit = () => {
      console.log({
        membershipCode: membershipCode.value,
        email: email.value,
        password: password.value,
        rememberMe: rememberMe.value,
      });
      // Add your login logic here
    };

    const openModal = () => {
      showModal.value = true;
    };

    const closeModal = () => {
      showModal.value = false;
    };

    return {
      membershipCode,
      email,
      password,
      rememberMe,
      showModal,
      handleSubmit,
      openModal,
      closeModal,
    };
  },
});
</script>

<!-- Scoped CSS, you can directly copy the styles from your CSS -->
<style scoped>
/* Copy your styles from the original CSS here */

* {
    box-sizing: border-box; /* Ensures consistent box model */
}

body, html {
    margin: 0;
    padding: 0;
    height: 100%;
}

.wrapper {
    display: flex;
    height: 100vh; /* Full viewport height */
    width: 100vw; /* Full viewport width */
}

.left-section {
    flex: 40%;
    background-color: black;
    display: flex;
    justify-content: center;
    align-items: center;
}

.left-content {
    text-align: center;
    color: white;
}

.left-content h1 {
    margin-bottom: 20px; /* Add space between lines */
}

.dont-have-account {
    font-size: 25px;
    margin-bottom: 33px; /* Add space between "Don't have an account?" and "Sign Up" */
}

.left-content a.signup-button {
    color: white;
    text-decoration: none;
    padding: 8px 16px;
    background-color: black; /* Background color black */
    border: 2px solid white; /* White border */
    border-radius: 5px; /* Rounded corners */
    transition: background-color 0.3s; /* Smooth transition */
}

.left-content a.signup-button:hover {
    background-color: #f44336; /* Red on hover */
}

.right-section {
    flex: 60%;
    background-color: #fff;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.login-container {
    width: 90%; /* Adjust the width of the login container */
    max-width: 570px; /* Adjust the maximum width of the login form */
    text-align: center; /* Center the logo */
}

.logo {
    max-width: 200px; /* Make the logo smaller */
    height: auto;
    margin-bottom: 20px;
}

input[type="text"],
input[type="email"],
input[type="password"],
button {
    width: 100%; /* Make input fields and button take the full width */
    box-sizing: border-box; /* Include padding and border in the element's total width and height */
    padding: 15px; /* Increase padding for inputs and button */
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
    transition: border-color 0.3s; /* Smooth transition for border color */
}

input[type="text"]:focus,
input[type="email"]:focus,
input[type="password"]:focus {
    border-color: #f44336;
    outline: none;
}


button {
    border: none; /* Remove border */
    background-color: #f44336; /* Red */
    color: #fff;
    cursor: pointer;
    font-size: 16px; /* Increase font size for better readability */
}

button:hover {
    background-color: #d32f2f; /* Darker red on hover */
}

.remember-forgot-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
}

.remember-forgot-container label {
    display: flex;
    align-items: center;
    cursor: pointer;
    font-size: 14px; /* Set the font size to match the checkbox */
}

.checkbox input {
    cursor: pointer;
    accent-color: #f44336; /* Red color for the checkbox */
}

input[type="checkbox"], input[type="radio"] {
    box-sizing: border-box;
    padding: 0;
}

.forgot-password {
    font-size: 14px; /* Match the font size of Remember Me text */
    color: #f44336; /* Red color for "Forgot Password?" link */
}

.remember-forgot-container a {
    color: #f44336;
    text-decoration: none;
}

.remember-forgot-container a:hover {
    color: #d32f2f; /* Darker red on hover */
}

.terms-text {
    font-size: 12px;
    color: #666;
    margin-top: 15px;
}

.terms-text a {
    color: #f44336; /* Red links */
    text-decoration: none;
}

.terms-text a:hover {
    text-decoration: underline;
}

</style>
