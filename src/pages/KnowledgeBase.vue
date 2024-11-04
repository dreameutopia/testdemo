<script setup>
import { ref } from 'vue'
import NavBar from '../components/NavBar.vue'

const conversations = ref([
  { id: 1, title: 'General Discussion', timestamp: '2024-03-20', content: 'Content 1...' },
  { id: 2, title: 'Coding Help', timestamp: '2024-03-19', content: 'Content 2...' },
  { id: 3, title: 'Project Ideas', timestamp: '2024-03-18', content: 'Content 3...' },
  // Add more items to demonstrate scrolling
  ...Array.from({ length: 10 }, (_, i) => ({
    id: i + 4,
    title: `Conversation ${i + 4}`,
    timestamp: '2024-03-17',
    content: `Content ${i + 4}...`
  }))
])

const selectedConversations = ref([])
const requirements = ref('')

const toggleSelection = (id) => {
  const index = selectedConversations.value.indexOf(id)
  if (index === -1) {
    selectedConversations.value.push(id)
  } else {
    selectedConversations.value.splice(index, 1)
  }
}

const generateKnowledgeBase = () => {
  // Implementation for knowledge base generation
  console.log('Generating knowledge base...')
}
</script>

<template>
  <div class="knowledge-base">
    <NavBar />
    <div class="container">
      <div class="header">
        <h1>Knowledge Base Generator</h1>
        <p>Select conversations and specify requirements to generate your knowledge base</p>
      </div>

      <div class="main-content">
        <div class="conversations-section">
          <h2>Available Conversations</h2>
          <div class="conversations-list">
            <div 
              v-for="chat in conversations" 
              :key="chat.id"
              class="conversation-item"
            >
              <label class="checkbox-container">
                <input 
                  type="checkbox" 
                  :checked="selectedConversations.includes(chat.id)"
                  @change="toggleSelection(chat.id)"
                >
                <span class="checkmark"></span>
                <div class="conversation-details">
                  <span class="title">{{ chat.title }}</span>
                  <span class="date">{{ chat.timestamp }}</span>
                </div>
              </label>
              <div class="preview">{{ chat.content }}</div>
            </div>
          </div>
        </div>

        <div class="requirements-section">
          <h2>Requirements</h2>
          <textarea
            v-model="requirements"
            placeholder="Specify your requirements for the knowledge base generation..."
            rows="6"
          ></textarea>

          <button 
            class="generate-btn"
            @click="generateKnowledgeBase"
            :disabled="selectedConversations.length === 0 || !requirements.trim()"
          >
            Generate Knowledge Base
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.knowledge-base {
  min-height: 100vh;
  background-color: #f7f7f8;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.header {
  text-align: center;
  margin-bottom: 2rem;
}

.header h1 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 0.5rem;
}

.header p {
  color: #666;
}

.main-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.conversations-section, .requirements-section {
  display: flex;
  flex-direction: column;
}

h2 {
  font-size: 1.2rem;
  color: #333;
  margin-bottom: 1rem;
}

.conversations-list {
  flex: 1;
  overflow-y: auto;
  max-height: 600px;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
}

.conversation-item {
  padding: 1rem;
  border-bottom: 1px solid #e5e5e5;
}

.conversation-item:last-child {
  border-bottom: none;
}

.checkbox-container {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.conversation-details {
  display: flex;
  justify-content: space-between;
  flex: 1;
}

.title {
  font-weight: 500;
}

.date {
  color: #666;
  font-size: 0.9rem;
}

.preview {
  margin-top: 0.5rem;
  color: #666;
  font-size: 0.9rem;
}

textarea {
  width: 100%;
  padding: 1rem;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  resize: vertical;
  margin-bottom: 1rem;
  font-family: inherit;
}

.generate-btn {
  padding: 1rem;
  background-color: #10a37f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.2s;
}

.generate-btn:hover:not(:disabled) {
  background-color: #0e906f;
}

.generate-btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

/* Custom checkbox styles */
.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

.checkmark {
  height: 20px;
  width: 20px;
  background-color: #fff;
  border: 2px solid #10a37f;
  border-radius: 4px;
  position: relative;
}

.checkbox-container:hover input ~ .checkmark {
  background-color: #f0f9f6;
}

.checkbox-container input:checked ~ .checkmark {
  background-color: #10a37f;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-container .checkmark:after {
  left: 6px;
  top: 2px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}
</style>