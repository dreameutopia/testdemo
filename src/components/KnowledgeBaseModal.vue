<script setup>
import { ref } from 'vue'

const props = defineProps({
  conversations: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['close'])

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
  // Here you would implement the actual knowledge base generation
  console.log('Selected conversations:', selectedConversations.value)
  console.log('Requirements:', requirements.value)
  emit('close')
}
</script>

<template>
  <div class="modal-overlay" @click="emit('close')">
    <div class="modal-content" @click.stop>
      <div class="modal-header">
        <h2>Generate Knowledge Base</h2>
        <button class="close-btn" @click="emit('close')">×</button>
      </div>
      
      <div class="modal-body">
        <div class="section">
          <h3>Select Conversations</h3>
          <div class="conversation-list">
            <div 
              v-for="chat in conversations" 
              :key="chat.id"
              class="conversation-checkbox"
            >
              <label>
                <input 
                  type="checkbox" 
                  :checked="selectedConversations.includes(chat.id)"
                  @change="toggleSelection(chat.id)"
                >
                <span class="checkbox-label">
                  {{ chat.title }}
                  <span class="date">{{ chat.timestamp }}</span>
                </span>
              </label>
            </div>
          </div>
        </div>

        <div class="section">
          <h3>Requirements</h3>
          <textarea
            v-model="requirements"
            placeholder="Enter your specific requirements for the knowledge base..."
            rows="4"
          ></textarea>
        </div>
      </div>

      <div class="modal-footer">
        <button class="cancel-btn" @click="emit('close')">Cancel</button>
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
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background-color: #ffffff;
  border-radius: 8px;
  width: 90%;
  max-width: 600px;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
}

.modal-header {
  padding: 1rem;
  border-bottom: 1px solid #e5e5e5;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-header h2 {
  margin: 0;
  font-size: 1.2rem;
  color: #333;
}

.close-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #666;
}

.modal-body {
  padding: 1rem;
  overflow-y: auto;
  flex: 1;
}

.section {
  margin-bottom: 1.5rem;
}

.section h3 {
  margin: 0 0 0.8rem 0;
  font-size: 1rem;
  color: #333;
}

.conversation-list {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  max-height: 200px;
  overflow-y: auto;
}

.conversation-checkbox {
  padding: 0.5rem;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.conversation-checkbox:hover {
  background-color: #f5f5f5;
}

.conversation-checkbox label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.checkbox-label {
  display: flex;
  justify-content: space-between;
  flex: 1;
  font-size: 0.9rem;
}

.date {
  color: #666;
  font-size: 0.8rem;
}

textarea {
  width: 100%;
  padding: 0.8rem;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  resize: vertical;
  font-family: inherit;
  font-size: 0.9rem;
}

textarea:focus {
  outline: none;
  border-color: #10a37f;
}

.modal-footer {
  padding: 1rem;
  border-top: 1px solid #e5e5e5;
  display: flex;
  justify-content: flex-end;
  gap: 0.8rem;
}

.cancel-btn {
  padding: 0.6rem 1rem;
  background-color: transparent;
  border: 1px solid #e5e5e5;
  color: #666;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.2s;
}

.cancel-btn:hover {
  background-color: #f5f5f5;
}

.generate-btn {
  padding: 0.6rem 1rem;
  background-color: #10a37f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background-color 0.2s;
}

.generate-btn:hover:not(:disabled) {
  background-color: #0e906f;
}

.generate-btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>