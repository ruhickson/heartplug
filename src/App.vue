<template>
  <div class="app">
    <template v-if="$route.path !== '/'">
      <div class="top-bar">
        <div class="logo-area">
          <svg class="heart" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
            <path d="M16 28.5c-.3 0-.6-.1-.8-.3C13.3 26.3 4 18.2 4 11.5 4 6.8 7.8 3 12.5 3c2.4 0 4.6 1.1 6 2.8 1.4-1.7 3.6-2.8 6-2.8C29.2 3 33 6.8 33 11.5c0 6.7-9.3 14.8-11.2 16.7-.2.2-.5.3-.8.3z" fill="#9b4dca"/>
          </svg>
          <svg class="plug" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M16 7V3H14V7H10V3H8V7H4V9H8V13H4V15H8V19H10V15H14V19H16V15H20V13H16V9H20V7H16Z" fill="#9b4dca"/>
          </svg>
        </div>
        <HamburgerMenu />
      </div>
    </template>
    <router-view />
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'
import HamburgerMenu from './components/HamburgerMenu.vue'
const $route = useRoute()
</script>

<style>
.app {
  min-height: 100vh;
  width: 100vw;
  background: linear-gradient(135deg, #9b4dca 0%, #ff69b4 60%, #ff69b4 100%);
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  position: relative;
}
.top-bar {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 1.5rem 2rem 0.5rem 2rem;
  position: relative;
  z-index: 10;
}
.logo-area {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.heart {
  width: 40px;
  height: 40px;
}
.plug {
  width: 24px;
  height: 24px;
}
</style> 