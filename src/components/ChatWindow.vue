<script setup>
import { defineProps, defineEmits } from 'vue'
import ToolBar from './ToolBar.vue'
import NavBar from './NavBar.vue'

const props = defineProps({
  messages: {
    type: Array,
    required: true
  },
  modelValue: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['update:modelValue', 'send'])

const handleInput = (e) => {
  emit('update:modelValue', e.target.value)
}

const handleSubmit = () => {
  emit('send')
}

const handleKeydown = (e) => {
  if (e.key === 'Enter' && !e.shiftKey) {
    e.preventDefault()
    handleSubmit()
  }
}
</script>

<template>
  <div class="chat-window">
    <NavBar />
    <div class="messages">
      <div 
        v-for="message in messages" 
        :key="message.id"
        :class="['message', message.role]"
      >
        <div class="message-content">
          {{ message.content }}
        </div>
      </div>
    </div>
    <div class="input-container">
      <ToolBar />
      <div class="input-area">
        <textarea
          :value="modelValue"
          @input="handleInput"
          @keydown="handleKeydown"
          placeholder="Type your message here..."
          rows="1"
        ></textarea>
        <button @click="handleSubmit" :disabled="!modelValue.trim()">
          Send
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.chat-window {
  flex: 1;
  display: flex;
  flex-direction: column;
  height: 100%;
  background-color: #ffffff;
}

.messages {
  flex: 1;
  overflow-y: auto;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.message {
  max-width: 80%;
  padding: 1rem;
  border-radius: 8px;
  line-height: 1.5;
}

.message.user {
  background-color: #10a37f;
  color: white;
  align-self: flex-end;
}

.message.assistant {
  background-color: #f7f7f8;
  color: #333;
  align-self: flex-start;
}

.input-container {
  border-top: 1px solid #e5e5e5;
}

.input-area {
  padding: 1rem;
  display: flex;
  gap: 0.5rem;
  background-color: #ffffff;
}

textarea {
  flex: 1;
  padding: 0.8rem;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  resize: none;
  font-family: inherit;
  font-size: 0.9rem;
  line-height: 1.5;
}

textarea:focus {
  outline: none;
  border-color: #10a37f;
}

button {
  padding: 0.8rem 1.2rem;
  background-color: #10a37f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background-color 0.2s;
}

button:hover:not(:disabled) {
  background-color: #0e906f;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>