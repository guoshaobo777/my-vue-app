<script setup>
import { ref, onMounted } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const themes = ['dark', 'light', 'orange']
const themeIndex = ref(0)
const themeIcons = ['🌙', '☀️', '🍊']

onMounted(() => {
  const saved = localStorage.getItem('theme')
  if (saved) {
    themeIndex.value = themes.indexOf(saved)
    if (themeIndex.value === -1) themeIndex.value = 0
  }
  applyTheme()
})

function toggleTheme() {
  themeIndex.value = (themeIndex.value + 1) % themes.length
  const currentTheme = themes[themeIndex.value]
  localStorage.setItem('theme', currentTheme)
  applyTheme()
}

function applyTheme() {
  document.documentElement.setAttribute('data-theme', themes[themeIndex.value])
}
</script>

<template>
  <button class="theme-toggle" @click="toggleTheme">
    {{ themeIcons[themeIndex] }}
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
