<template>
  <div class="app">
    <FloatingBlockchains />
    <CenterText />
    <HeartAnimation />
    <div style="height: 200vh;"></div>
  </div>
</template>

<script setup>
import HeartAnimation from './components/HeartAnimation.vue'
import FloatingBlockchains from './components/FloatingBlockchains.vue'
import CenterText from './components/CenterText.vue'
</script>

<style>
html, body, #app {
  width: 100vw;
  margin: 0;
  padding: 0;
}

.app {
  min-height: 100vh;
  width: 100vw;
  background: linear-gradient(135deg, #9b4dca, #ff69b4);
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style> 