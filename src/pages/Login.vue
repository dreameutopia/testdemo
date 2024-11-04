<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')

const handleLogin = () => {
  // Implementation for login
  console.log('Logging in...')
}
</script>

<template>
  <div class="auth-page">
    <div class="auth-container">
      <div class="auth-box">
        <h1>Welcome Back</h1>
        <p class="subtitle">Log in to your account</p>

        <form @submit.prevent="handleLogin" class="auth-form">
          <div class="form-group">
            <label for="email">Email</label>
            <input
              id="email"
              type="email"
              v-model="email"
              required
              placeholder="Enter your email"
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

          <div class="form-footer">
            <label class="remember-me">
              <input type="checkbox">
              <span>Remember me</span>
            </label>
            <a href="#" class="forgot-password">Forgot password?</a>
          </div>

          <button type="submit" class="submit-btn">Log In</button>
        </form>

        <p class="switch-auth">
          Don't have an account? <a href="/register">Sign up</a>
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

.form-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.9rem;
}

.remember-me {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.forgot-password {
  color: #10a37f;
  text-decoration: none;
}

.forgot-password:hover {
  text-decoration: underline;
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