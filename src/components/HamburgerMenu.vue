<template>
  <div class="hamburger-menu">
    <button class="hamburger" @click="open = !open" aria-label="Open menu">
      <span></span><span></span><span></span>
    </button>
    <div v-if="open" class="menu-overlay" @click.self="open = false">
      <nav class="menu">
        <router-link v-for="item in items" :key="item.text" :to="item.to" class="menu-item" @click="open = false">
          {{ item.text }}
        </router-link>
      </nav>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const open = ref(false)
const items = [
  { text: 'Home', to: '/' },
  { text: 'What it is', to: '/what-it-is' },
  { text: 'How it works', to: '/how-it-works' },
  { text: 'Who it\'s for', to: '/who-its-for' },
  { text: 'How to get it', to: '/how-to-get-it' },
  { text: 'About', to: '/about' },
  { text: 'Contact', to: '/contact' },
]
</script>

<style scoped>
.hamburger-menu {
  position: relative;
  z-index: 100;
}
.hamburger {
  background: none;
  border: none;
  cursor: pointer;
  width: 40px;
  height: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 6px;
  padding: 0;
}
.hamburger span {
  display: block;
  width: 28px;
  height: 4px;
  background: #fff;
  border-radius: 2px;
  transition: all 0.3s;
}
.menu-overlay {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(20, 20, 40, 0.7);
  display: flex;
  justify-content: flex-end;
  z-index: 99;
}
.menu {
  background: #222b44;
  min-width: 220px;
  padding: 2rem 1.5rem;
  border-radius: 0 0 0 16px;
  margin-top: 0;
  margin-right: 0;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  box-shadow: -2px 0 16px #0004;
  height: 100vh;
}
.menu-item {
  color: #fff;
  font-size: 1.2rem;
  font-weight: 600;
  text-decoration: none;
  transition: color 0.2s;
  padding: 0.2em 0;
}
.menu-item:hover {
  color: #ff69b4;
}
</style> 