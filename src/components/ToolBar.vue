<script setup>
const tools = [
  { id: 'image', icon: '📷', label: 'Image' },
  { id: 'file', icon: '📎', label: 'Attach' },
  { id: 'code', icon: '💻', label: 'Code' },
  { id: 'voice', icon: '🎤', label: 'Voice' }
]
</script>

<template>
  <div class="toolbar">
    <button 
      v-for="tool in tools" 
      :key="tool.id"
      class="tool-button"
      :title="tool.label"
    >
      <span class="tool-icon">{{ tool.icon }}</span>
    </button>
  </div>
</template>

<style scoped>
.toolbar {
  display: flex;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  border-bottom: 1px solid #e5e5e5;
}

.tool-button {
  background: transparent;
  border: none;
  padding: 0.5rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.tool-button:hover {
  background-color: #f0f0f0;
}

.tool-icon {
  font-size: 1.2rem;
}
</style>