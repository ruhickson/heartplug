<template>
  <div class="floating-blockchains">
    <template v-if="messageIndex === 3">
      <div class="orbit">
        <span
          v-for="(chain, i) in chains"
          :key="chain.id"
          class="blockchain-name orbiting"
          :style="orbitStyle(i)"
        >
          {{ chain.name }}
        </span>
      </div>
    </template>
    <template v-else>
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
    </template>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const props = defineProps({ messageIndex: Number })

const blockchainNames = [
  'bitcoin', 'ethereum', 'bnb', 'solana', 'cardano', 'xrp', 'polkadot', 'dogecoin', 'tron', 'avalanche', 'polygon', 'litecoin', 'stellar', 'chainlink', 'cosmos', 'uniswap', 'tezos', 'vechain', 'aptos', 'near', 'arbitrum', 'optimism', 'fantom', 'hedera', 'algorand', 'elrond', 'iota', 'zcash', 'monero', 'dash', 'kusama', 'flow', 'waves', 'neo', 'thorchain', 'celo', 'chiliz', 'mina', 'loopring', 'decred', 'nervos', 'harmony', 'icon', 'theta', 'ontology', 'qtum', 'ravencoin', 'zilliqa', 'ankr', 'eos', 'lisk', 'oasis', 'energyweb', 'injective', 'kava', 'bitshares', 'syscoin', 'wax', 'aurora', 'radix', 'multiversx', 'dydx', 'immutablex', 'sui', 'mantle', 'metis', 'coreum', 'akash', 'band', 'boba', 'clover', 'biconomy', 'skale', 'godwoken', 'moonbeam', 'moonriver', 'scroll', 'linea', 'base', 'zksync', 'starknet', 'sepolia', 'goerli', 'evmos', 'flare', 'rootstock', 'kcc', 'telos', 'fusion', 'persistence', 'stratis', 'celer', 'ultra', 'verge', 'axiom', 'quarkchain', 'sora', 'safe', 'bitcoin-cash', 'smartbch', 'ronin', 'bitgert',
  'shardium', 'nuls', 'ontology-gas', 'beldex', 'hydra', 'dfinity', 'kaspa', 'celer-network', 'beam', 'grin', 'metadium', 'orbit-chain', 'canto', 'platon', 'findora', 'celer', 'uquid', 'functionx', 'zenon', 'wanchain', 'bluzelle', 'stratis', 'credits', 'proton', 'tomochain', 'telcoin', 'telos', 'safepal', 'safemoon', 'vite', 'velas', 'callisto', 'xdag', 'fio', 'insolar', 'freicoin', 'peercoin', 'emercoin', 'navcoin', 'nxt', 'waves-ducks', 'bytom', 'ardor', 'komodo', 'bitbay', 'maidsafecoin', 'factom', 'namecoin', 'counterparty', 'omniledger', 'burst', 'yocoin', 'ixcoin', 'feathercoin', 'clams', 'terracoin', 'mintcoin', 'blackcoin', 'vericoin', 'rubycoin', 'potcoin', 'quark', 'infinitecoin', 'mooncoin', 'espers', 'okcash', 'neblio', 'radium', 'ubiq', 'phoenixcoin', 'primecoin', 'gridcoin', 'diamond', 'denarius', 'turtlecoin', 'cryptonote', 'monacoin', 'electroneum', 'sumokoin', 'aeon', 'karbo', 'tixl', 'nexa', 'firo', 'particl', 'spectrecoin', 'nav', 'smartcash', 'whitecoin', 'myriad', 'expanse', 'cloakcoin', 'syndicate', 'boolberry', 'hypercash', 'digibyte', 'reddcoin', 'feather', 'graft', 'tenset', 'strongblock'
]

const chains = ref([])
const numChains = 250
const minFont = 8
const maxFont = 18
const speedMin = 0.05
const speedMax = 0.2
let animationFrame

function randomX() {
  let x
  do {
    x = Math.random() * 90
  } while (x > 30 && x < 60)
  return x
}

function randomChain(i) {
  return {
    id: i + '-' + Math.random().toString(36).slice(2),
    name: blockchainNames[Math.floor(Math.random() * blockchainNames.length)],
    x: randomX(), // vw
    y: Math.random() * 100, // vh
    size: Math.floor(Math.random() * (maxFont - minFont + 1)) + minFont,
    speed: Math.random() * (speedMax - speedMin) + speedMin,
  }
}

function resetChain(chain) {
  chain.x = randomX()
  chain.y = 100
  chain.size = Math.floor(Math.random() * (maxFont - minFont + 1)) + minFont
  chain.speed = Math.random() * (speedMax - speedMin) + speedMin
  chain.name = blockchainNames[Math.floor(Math.random() * blockchainNames.length)]
}

function animate() {
  if (props.messageIndex !== 3) {
    for (const chain of chains.value) {
      chain.y -= chain.speed
      if (chain.y < -5) {
        resetChain(chain)
      }
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

// Orbiting style for each blockchain (CSS transform)
const orbitStyle = (i) => {
  const radius = (240 + (i % 3) * 40) * 2 // px, doubled radius
  const angle = (i / numChains) * 360
  const fontSize = Math.floor(Math.random() * (maxFont - minFont + 1)) + minFont
  return {
    position: 'absolute',
    left: '50%',
    top: '50%',
    transform: `rotate(${angle}deg) translate(${radius}px)`,
    fontSize: fontSize + 'px',
    pointerEvents: 'none',
    opacity: 0.85,
    whiteSpace: 'nowrap',
  }
}
</script>

<style scoped>
.floating-blockchains {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  pointer-events: none;
  z-index: 20; /* Increased to ensure above overlays */
}
.blockchain-name {
  position: absolute;
  color: rgba(255,255,255,0.85);
  font-family: monospace, sans-serif;
  user-select: none;
  white-space: nowrap;
  font-weight: bold;
  text-shadow: 0 1px 4px #9b4dca44;
  opacity: 0.85 !important; /* Always visible */
  transition: none !important;
}
.orbit {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  pointer-events: none;
  z-index: 20; /* Increased to ensure above overlays */
  animation: orbit-rotate 64s linear infinite;
  transform-origin: 50vw 50vh;
}
.orbiting {
  will-change: transform;
}
@keyframes orbit-rotate {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style> 