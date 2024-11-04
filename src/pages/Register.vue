<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const verificationCode = ref('')
const isCodeSent = ref(false)
const countdown = ref(0)

const sendVerificationCode = () => {
  if (countdown.value > 0) return
  
  // Implementation for sending verification code
  console.log('Sending verification code...')
  isCodeSent.value = true
  countdown.value = 60
  
  const timer = setInterval(() => {
    countdown.value--
    if (countdown.value === 0) {
      clearInterval(timer)
    }
  }, 1000)
}

const handleRegister = () => {
  // Implementation for registration
  console.log('Registering...')
}
</script>

<template>
  <div class="auth-page">
    <div class="auth-container">
      <div class="auth-box">
        <h1>Create Account</h1>
        <p class="subtitle">Sign up for a new account</p>

        <form @submit.prevent="handleRegister" class="auth-form">
          <div class="form-group">
            <label for="email">Email</label>
            <div class="email-group">
              <input
                id="email"
                type="email"
                v-model="email"
                required
                placeholder="Enter your email"
              >
              <button 
                type="button" 
                class="verify-btn" 
                @click="sendVerificationCode"
                :disabled="countdown > 0"
              >
                {{ countdown > 0 ? `${countdown}s` : 'Get Code' }}
              </button>
            </div>
          </div>

          <div class="form-group" v-if="isCodeSent">
            <label for="verification">Verification Code</label>
            <input
              id="verification"
              type="text"
              v-model="verificationCode"
              required
              placeholder="Enter verification code"
              maxlength="6"
            >
          </div>

          <div class="form-group">
            <label for="password">Password</label>
            <input
              id="password"
              type="password"
              v-model="password"
              required
              placeholder="Enter your password"
            >
          </div>

          <div class="form-group">
            <label for="confirm-password">Confirm Password</label>
            <input
              id="confirm-password"
              type="password"
              v-model="confirmPassword"
              required
              placeholder="Confirm your password"
            >
          </div>

          <button type="submit" class="submit-btn">Create Account</button>
        </form>

        <p class="switch-auth">
          Already have an account? <a href="/login">Log in</a>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.auth-page {
  min-height: 100vh;
  background-color: #f7f7f8;
  display: flex;
  align-items: center;
  justify-content: center;
}

.auth-container {
  width: 100%;
  max-width: 400px;
  padding: 1rem;
}

.auth-box {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  font-size: 1.8rem;
  color: #333;
  margin-bottom: 0.5rem;
  text-align: center;
}

.subtitle {
  color: #666;
  text-align: center;
  margin-bottom: 2rem;
}

.auth-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.email-group {
  display: flex;
  gap: 0.5rem;
}

.email-group input {
  flex: 1;
}

label {
  font-size: 0.9rem;
  color: #333;
}

input {
  padding: 0.8rem;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  font-size: 1rem;
}

input:focus {
  outline: none;
  border-color: #10a37f;
}

.verify-btn {
  padding: 0 1rem;
  background-color: #10a37f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  white-space: nowrap;
  transition: background-color 0.2s;
}

.verify-btn:hover:not(:disabled) {
  background-color: #0e906f;
}

.verify-btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.submit-btn {
  padding: 1rem;
  background-color: #10a37f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.2s;
}

.submit-btn:hover {
  background-color: #0e906f;
}

.switch-auth {
  margin-top: 1.5rem;
  text-align: center;
  font-size: 0.9rem;
}

.switch-auth a {
  color: #10a37f;
  text-decoration: none;
}

.switch-auth a:hover {
  text-decoration: underline;
}
</style>