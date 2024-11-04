<script setup>
const modelName = "GPT-4 Turbo"
</script>

<template>
  <div class="navbar">
    <div class="model-name">{{ modelName }}</div>
    <div class="auth-buttons">
      <button class="login-btn">Login</button>
      <button class="register-btn">Register</button>
    </div>
  </div>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.8rem 1.5rem;
  background-color: #ffffff;
  border-bottom: 1px solid #e5e5e5;
}

.model-name {
  font-size: 1.1rem;
  font-weight: 600;
  color: #333;
}

.auth-buttons {
  display: flex;
  gap: 0.8rem;
}

.auth-buttons button {
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.2s;
}

.login-btn {
  background-color: transparent;
  border: 1px solid #10a37f;
  color: #10a37f;
}

.login-btn:hover {
  background-color: #f0f9f6;
}

.register-btn {
  background-color: #10a37f;
  border: 1px solid #10a37f;
  color: white;
}

.register-btn:hover {
  background-color: #0e906f;
}
</style>