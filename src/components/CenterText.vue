<template>
  <div class="center-text">
    <transition name="fade" mode="out-in">
      <span :key="message">{{ message }}</span>
    </transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const message = ref('What happens to your cryptocurrency after you die?')

function onScroll() {
  if (window.scrollY > 0) {
    message.value = 'Does anyone get it, or does it disappear into the aether?'
  } else {
    message.value = 'What happens to your cryptocurrency after you die?'
  }
}

onMounted(() => {
  window.addEventListener('scroll', onScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
})
</script>

<style scoped>
.center-text {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 10;
  color: #fff;
  font-size: 2rem;
  font-family: 'Inter', Arial, sans-serif;
  text-align: center;
  text-shadow: 0 2px 16px #9b4dca88;
  pointer-events: none;
  max-width: 90vw;
  font-weight: 600;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.7s cubic-bezier(.4,0,.2,1);
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style> 