<template>
  <div class="floating-blockchains">
    <span
      v-for="(chain, i) in chains"
      :key="chain.id"
      class="blockchain-name"
      :style="{
        left: chain.x + 'vw',
        top: chain.y + 'vh',
        fontSize: chain.size + 'px',
        transition: 'none',
      }"
    >
      {{ chain.name }}
    </span>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const blockchainNames = [
  'ethereum', 'bitcoin', 'solana', 'polygon', 'avalanche', 'arbitrum', 'optimism', 'tron', 'binance', 'fantom',
  'cardano', 'polkadot', 'near', 'tezos', 'algorand', 'cosmos', 'hedera', 'elrond', 'celo', 'harmony',
  'kava', 'waves', 'flow', 'stacks', 'zilliqa', 'vechain', 'eos', 'ontology', 'qtum', 'icon'
]

const chains = ref([])
const numChains = 30
const minFont = 8
const maxFont = 18
const speedMin = 0.05
const speedMax = 0.2
let animationFrame

function randomChain(i) {
  return {
    id: i + '-' + Math.random().toString(36).slice(2),
    name: blockchainNames[Math.floor(Math.random() * blockchainNames.length)],
    x: Math.random() * 90, // vw
    y: Math.random() * 100, // vh
    size: Math.floor(Math.random() * (maxFont - minFont + 1)) + minFont,
    speed: Math.random() * (speedMax - speedMin) + speedMin,
  }
}

function resetChain(chain) {
  chain.x = Math.random() * 90
  chain.y = 100
  chain.size = Math.floor(Math.random() * (maxFont - minFont + 1)) + minFont
  chain.speed = Math.random() * (speedMax - speedMin) + speedMin
  chain.name = blockchainNames[Math.floor(Math.random() * blockchainNames.length)]
}

function animate() {
  for (const chain of chains.value) {
    chain.y -= chain.speed
    if (chain.y < -5) {
      resetChain(chain)
    }
  }
  animationFrame = requestAnimationFrame(animate)
}

onMounted(() => {
  chains.value = Array.from({ length: numChains }, (_, i) => randomChain(i))
  animate()
})

onUnmounted(() => {
  cancelAnimationFrame(animationFrame)
})
</script>

<style scoped>
.floating-blockchains {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  pointer-events: none;
  z-index: 1;
}
.blockchain-name {
  position: absolute;
  color: rgba(255,255,255,0.25);
  font-family: monospace, sans-serif;
  user-select: none;
  white-space: nowrap;
  font-weight: bold;
  text-shadow: 0 1px 4px #9b4dca44;
}
</style> 