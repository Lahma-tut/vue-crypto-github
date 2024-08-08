<script setup>
import { ref } from 'vue';

const props = defineProps({
  setCrypto: {
    type: Function,
    required: true
  },
  cryptoNow: {
    type: String,
    required: true
  }
})

</script>

<template>
  <ul>
    <li @click="setCrypto('BTC')" :class="cryptoNow == 'BTC' ? 'active' : ''">Bitcoin</li>
    <li @click="setCrypto('ETH')" :class="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
    <li @click="setCrypto('USDT')" :class="cryptoNow == 'USDT' ? 'active' : ''">USDT</li>
  </ul>
</template>

<style scoped>
ul {
  width: 100%;
  list-style: none;
  padding: 0;
  border-radius: 2px;
  background: #f1f1f1;
}

li {
  display: block;
  padding: 20px 0;
  font-size: 1em;
  color: #333;
  transition: all 0.5s ease;
}

li:hover {
  border-radius: 2px;
  background: #fdbb2db1;
  cursor: pointer;
}

.active {
  border-radius: 2px;
  background: #fdbb2db1;
  cursor: pointer;
}
</style>
