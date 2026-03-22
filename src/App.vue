<script setup>
import { ref, onMounted } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const isDark = ref(true)

onMounted(() => {
  const saved = localStorage.getItem('theme')
  isDark.value = saved ? saved === 'dark' : true
  applyTheme()
})

function toggleTheme() {
  isDark.value = !isDark.value
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
  applyTheme()
}

function applyTheme() {
  document.documentElement.setAttribute('data-theme', isDark.value ? 'dark' : 'light')
}
</script>

<template>
  <button class="theme-toggle" @click="toggleTheme">
    {{ isDark ? '☀️' : '🌙' }}
  </button>
  <HelloWorld />
</template>

<style scoped>
.theme-toggle {
  position: fixed;
  top: 16px;
  right: 16px;
  z-index: 999;
  font-size: 1.5rem;
  background: transparent;
  border: 2px solid var(--color-border, #ccc);
  border-radius: 50%;
  width: 48px;
  height: 48px;
  cursor: pointer;
  transition: transform 0.3s ease;
}
.theme-toggle:hover {
  transform: scale(1.15);
}
</style>
