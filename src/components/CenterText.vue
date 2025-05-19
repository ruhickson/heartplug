<template>
  <div class="center-text">
    <transition name="fade" mode="out-in">
      <span :key="messageIndex">
        <template v-if="messageIndex < 3">
          {{ messages[messageIndex] }}
        </template>
        <template v-else>
          {{ messages[3] }}<br /><br />
          <a href="/about" class="find-out-link">Find out more now</a>
        </template>
      </span>
    </transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch, defineEmits } from 'vue'

const emit = defineEmits(['update:messageIndex'])

const messages = [
  'What happens to your cryptocurrency after you die?',
  'Does anyone get it, or does it disappear into the aether?',
  'Do your loved ones have access to your private keys? Your wealth? Their future financial security?',
  'With heartplug, you can stop worrying about the future and make the most of the now.'
]

const messageIndex = ref(0)

function onScroll() {
  const y = window.scrollY
  if (y < 200) {
    messageIndex.value = 0
  } else if (y < 600) {
    messageIndex.value = 1
  } else if (y < 1000) {
    messageIndex.value = 2
  } else {
    messageIndex.value = 3
  }
}

watch(messageIndex, (val) => {
  emit('update:messageIndex', val)
})

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
.find-out-link {
  color: #fff;
  font-size: 2rem;
  font-weight: 700;
  text-decoration: none;
  pointer-events: auto;
  cursor: pointer;
  display: inline-block;
  margin-top: 0;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.7s cubic-bezier(.4,0,.2,1);
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style> 