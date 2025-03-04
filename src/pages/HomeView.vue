<template>
    <div class="container">
      <!-- Tabs to toggle between Sign In and Sign Up -->
      <div class="tabs">
        <button @click="showSignIn" :class="{ active: isSignIn }">Sign In</button>
        <button @click="showSignUp" :class="{ active: !isSignIn }">Sign Up</button>
      </div>

      <!-- Sign In Form -->
      <div v-if="isSignIn" class="form-container">
        <h2>Sign In</h2>
        <form @submit.prevent="handleSignInSubmit">
          <label for="signInEmail">Email:</label>
          <input type="email" id="signInEmail" v-model="signInData.email" required>

          <label for="signInPassword">Password:</label>
          <input type="password" id="signInPassword" v-model="signInData.password" required>

          <button type="submit">Sign In</button>
        </form>
      </div>

      <!-- Sign Up Form -->
      <div v-else class="form-container">
        <h2>Sign Up</h2>
        <form @submit.prevent="handleSignUpSubmit">
          <label for="signUpEmail">Email:</label>
          <input type="email" id="signUpEmail" v-model="signUpData.email" required>

          <label for="signUpPassword">Password:</label>
          <input type="password" id="signUpPassword" v-model="signUpData.password" required>

          <label for="confirmPassword">Confirm Password:</label>
          <input type="password" id="confirmPassword" v-model="signUpData.confirmPassword" required>

          <button type="submit">Sign Up</button>
        </form>
      </div>
    </div>
</template>
 
<script setup>
import { ref } from 'vue'
import axiosClient from '../axiosClient.js'

</script>



<style>

</style>