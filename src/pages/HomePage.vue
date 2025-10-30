<template>
  <div class="landing-app" :style="{ '--blue-overlay-opacity': blueOverlayOpacity }">
    <FloatingBlockchains :messageIndex="messageIndex" />
    <CenterText @update:messageIndex="onMessageIndex" />
    <HeartAnimation :messageIndex="messageIndex" />
    <div style="height: 400vh;"></div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import FloatingBlockchains from '../components/FloatingBlockchains.vue'
import CenterText from '../components/CenterText.vue'
import HeartAnimation from '../components/HeartAnimation.vue'

const messageIndex = ref(0)
const blueOverlayOpacity = ref(0)
function onMessageIndex(idx) {
  messageIndex.value = idx
}
function updateOverlay() {
  const y = window.scrollY
  if (y <= 1000) blueOverlayOpacity.value = 0
  else if (y >= 1300) blueOverlayOpacity.value = 1
  else blueOverlayOpacity.value = (y - 1000) / 300
}
onMounted(() => {
  window.addEventListener('scroll', updateOverlay)
})
onUnmounted(() => {
  window.removeEventListener('scroll', updateOverlay)
})
</script>

<style scoped>
.landing-app {
  min-height: 100vh;
  width: 100vw;
  background: linear-gradient(135deg, #9b4dca 0%, #ff69b4 60%, #ff69b4 100%);
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}
.landing-app::after {
  content: '';
  pointer-events: none;
  position: fixed;
  left: 0; top: 0; width: 100vw; height: 100vh;
  z-index: 2;
  background: linear-gradient(135deg, #1a355c 0%, #3a8dde 60%, #6be0ff 100%);
  opacity: var(--blue-overlay-opacity, 0);
  transition: opacity 0.8s cubic-bezier(.4,0,.2,1);
}
</style> 