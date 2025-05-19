<template>
  <div class="heart-container" ref="container">
    <div class="heart-wrapper">
      <svg class="heart" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
        <path :d="heartPath" :fill="heartColor"/>
      </svg>
      <svg class="plug" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M16 7V3H14V7H10V3H8V7H4V9H8V13H4V15H8V19H10V15H14V19H16V15H20V13H16V9H20V7H16Z" fill="#9b4dca"/>
      </svg>
    </div>
    <div v-for="(fragment, index) in fragments" 
         :key="index" 
         class="heart-fragment"
         :style="fragment.style">
      <svg viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
        <path :d="heartPath" :fill="heartColor"/>
      </svg>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
const props = defineProps({ messageIndex: Number })

const container = ref(null)
const fragments = ref([])
const scrollY = ref(typeof window !== 'undefined' ? window.scrollY : 0)
let animationFrame = null

const heartPath =
  'M16 28.5c-.3 0-.6-.1-.8-.3C13.3 26.3 4 18.2 4 11.5 4 6.8 7.8 3 12.5 3c2.4 0 4.6 1.1 6 2.8 1.4-1.7 3.6-2.8 6-2.8C29.2 3 33 6.8 33 11.5c0 6.7-9.3 14.8-11.2 16.7-.2.2-.5.3-.8.3z'

// Interpolate between purple and red based on scrollY
const heartColor = computed(() => {
  const y = scrollY.value
  const start = 1000
  const end = 1300
  let t = 0
  if (y <= start) t = 0
  else if (y >= end) t = 1
  else t = (y - start) / (end - start)
  // Interpolate RGB
  const from = { r: 155, g: 77, b: 202 } // #9b4dca
  const to = { r: 255, g: 59, b: 59 }   // #ff3b3b
  const r = Math.round(from.r + (to.r - from.r) * t)
  const g = Math.round(from.g + (to.g - from.g) * t)
  const b = Math.round(from.b + (to.b - from.b) * t)
  return `rgb(${r},${g},${b})`
})

const createFragment = () => {
  const size = Math.random() * 20 + 10
  const angle = Math.random() * 360
  const distance = Math.random() * 100 + 50
  const duration = Math.random() * 2 + 2

  return {
    style: {
      width: `${size}px`,
      height: `${size}px`,
      transform: `rotate(${angle}deg)`,
      animation: `float ${duration}s ease-out forwards`,
      left: '50%',
      top: '50%',
      '--distance': `${distance}px`,
      '--angle': `${angle}deg`,
    }
  }
}

const handleScroll = () => {
  scrollY.value = window.scrollY
  if (window.scrollY % 100 === 0) {
    fragments.value.push(createFragment())
    if (fragments.value.length > 20) {
      fragments.value.shift()
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.heart-container {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 5;
  width: auto;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

.heart-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  gap: 10px;
}

.heart {
  width: 100px;
  height: 100px;
  filter: drop-shadow(0 0 10px rgba(155, 77, 202, 0.5));
}

.plug {
  width: 40px;
  height: 40px;
  filter: drop-shadow(0 0 10px rgba(155, 77, 202, 0.5));
}

.heart-fragment {
  position: absolute;
  pointer-events: none;
  opacity: 0.6;
}

@keyframes float {
  0% {
    transform: translate(-50%, -50%) rotate(var(--angle));
    opacity: 0.6;
  }
  100% {
    transform: translate(
      calc(-50% + var(--distance) * cos(var(--angle))),
      calc(-50% + var(--distance) * sin(var(--angle)))
    ) rotate(var(--angle));
    opacity: 0;
  }
}
</style> 