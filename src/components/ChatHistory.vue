<script setup>
import { ref } from 'vue'
import KnowledgeBaseModal from './KnowledgeBaseModal.vue'

defineProps({
  conversations: {
    type: Array,
    required: true
  }
})

const isModalOpen = ref(false)

const openModal = () => {
  isModalOpen.value = true
}
</script>

<template>
  <div class="chat-history">
    <div class="header">
      <h2>Chat History</h2>
      <button class="new-chat">+ New Chat</button>
    </div>
    <div class="conversations">
      <div 
        v-for="chat in conversations" 
        :key="chat.id" 
        class="conversation-item"
      >
        <div class="chat-title">{{ chat.title }}</div>
        <div class="chat-date">{{ chat.timestamp }}</div>
      </div>
    </div>
    <div class="footer">
      <button class="knowledge-base-btn" @click="openModal">
        <span class="icon">📚</span>
        Knowledge Base
      </button>
    </div>
    <KnowledgeBaseModal 
      v-if="isModalOpen" 
      :conversations="conversations"
      @close="isModalOpen = false"
    />
  </div>
</template>

<style scoped>
.chat-history {
  width: 260px;
  background-color: #f7f7f8;
  border-right: 1px solid #e5e5e5;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.header {
  padding: 1rem;
  border-bottom: 1px solid #e5e5e5;
}

.header h2 {
  margin: 0;
  font-size: 1.2rem;
  color: #333;
  margin-bottom: 1rem;
}

.new-chat {
  width: 100%;
  padding: 0.5rem;
  background-color: #10a37f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
}

.new-chat:hover {
  background-color: #0e906f;
}

.conversations {
  overflow-y: auto;
  flex: 1;
}

.conversation-item {
  padding: 0.8rem 1rem;
  cursor: pointer;
  border-bottom: 1px solid #e5e5e5;
  transition: background-color 0.2s;
}

.conversation-item:hover {
  background-color: #ececec;
}

.chat-title {
  font-size: 0.9rem;
  color: #333;
  margin-bottom: 0.2rem;
}

.chat-date {
  font-size: 0.8rem;
  color: #666;
}

.footer {
  padding: 1rem;
  border-top: 1px solid #e5e5e5;
}

.knowledge-base-btn {
  width: 100%;
  padding: 0.8rem;
  background-color: #ffffff;
  border: 1px solid #10a37f;
  color: #10a37f;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  transition: all 0.2s;
}

.knowledge-base-btn:hover {
  background-color: #f0f9f6;
}

.icon {
  font-size: 1.2rem;
}
</style>