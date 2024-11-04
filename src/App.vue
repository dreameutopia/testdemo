<script setup>
import { ref } from 'vue'
import ChatHistory from './components/ChatHistory.vue'
import ChatWindow from './components/ChatWindow.vue'

const conversations = ref([
  { id: 1, title: 'General Discussion', timestamp: '2024-03-20' },
  { id: 2, title: 'Coding Help', timestamp: '2024-03-19' },
  { id: 3, title: 'Project Ideas', timestamp: '2024-03-18' }
])

const currentChat = ref({
  messages: [
    { id: 1, role: 'assistant', content: 'Hello! How can I help you today?' },
    { id: 2, role: 'user', content: 'Can you help me with Vue.js?' },
    { id: 3, role: 'assistant', content: 'Of course! What would you like to know about Vue.js?' }
  ]
})

const newMessage = ref('')

const sendMessage = () => {
  if (newMessage.value.trim()) {
    currentChat.value.messages.push({
      id: currentChat.value.messages.length + 1,
      role: 'user',
      content: newMessage.value
    })
    // Simulate assistant response
    setTimeout(() => {
      currentChat.value.messages.push({
        id: currentChat.value.messages.length + 1,
        role: 'assistant',
        content: 'This is a simulated response. In a real application, this would be connected to an API.'
      })
    }, 1000)
    newMessage.value = ''
  }
}
</script>

<template>
  <div class="app-container">
    <ChatHistory :conversations="conversations" />
    <ChatWindow 
      :messages="currentChat.messages"
      v-model="newMessage"
      @send="sendMessage"
    />
  </div>
</template>

<style>
.app-container {
  display: flex;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  background-color: #ffffff;
}
</style>