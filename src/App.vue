<script setup>
import { ref } from 'vue';
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Favourite from './components/Favourite.vue';
import CryptoConvert from 'crypto-convert';

const convertCurrency = new CryptoConvert()

const amount = ref(0)
const cryptoFirst = ref('')
const cryptoSecond = ref('')
const error = ref('')
const result = ref(0)
const favs = ref([])

function changeAmount(val) {
  amount.value = val
}

function setCryptoFirst(val) {
  cryptoFirst.value = val
}

function setCryptoSecond(val) {
  cryptoSecond.value = val
}

async function convert() {
  // оповещение об неправильном вводе или ошибке
  if(amount.value <= 0) {
    error.value = 'Введите число больше нуля'
    return
  } else if(cryptoFirst.value === cryptoSecond.value) {
    error.value = 'Выберите валюту для обмена'
    return
  } else if(cryptoFirst.value === '' || cryptoSecond.value === '' ) {
    error.value = 'Выберите валюту'
    return
  }

  error.value = ''

  // запускаем CryptoConvert
  await convertCurrency.ready()

  // перебираем валютные пары
  if(cryptoFirst.value === 'BTC' && cryptoSecond.value === 'ETH') {
    result.value = convertCurrency.BTC.ETH(amount.value)
  } else if(cryptoFirst.value === 'BTC' && cryptoSecond.value === 'USDT'){
    result.value = convertCurrency.BTC.USDT(amount.value)
  } else if(cryptoFirst.value === 'ETH' && cryptoSecond.value === 'BTC') {
    result.value = convertCurrency.ETH.BTC(amount.value)
  } else if(cryptoFirst.value === 'ETH' && cryptoSecond.value === 'USDT') {
    result.value = convertCurrency.ETH.USDT(amount.value)
  } else if(cryptoFirst.value === 'USDT' && cryptoSecond.value === 'BTC') {
    result.value = convertCurrency.USDT.BTC(amount.value)
  } else if(cryptoFirst.value === 'USDT' && cryptoSecond.value === 'ETH') {
    result.value = convertCurrency.USDT.ETH(amount.value)
  }
}

function favourite() {
  favs.value.push({
    from: cryptoFirst.value,
    to: cryptoSecond.value 
  })
}

function getFromFavs(index) {
  cryptoFirst.value = favs.value[index].from
  cryptoSecond.value = favs.value[index].to
}

</script>

<template>
  <header>
    <h1>Crypto</h1>
  </header>
  <main>

    <Input 
      :changeAmount="changeAmount" 
      :convert="convert" 
      :favourite="favourite"
      />

    <p v-if="error != ''">{{ error }}</p>
    <p v-if="result != 0" class="result">{{ result }} {{ cryptoSecond }}</p>

    <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
  
    <div class="selectors">
      <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
      <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
    </div>

  </main>
  <footer>

  </footer>
</template>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-between;
  width: 100%;
  gap: 20px;
}

.result {
  font-size: 2em;
  line-height: 1.1;
  font-family: "Bungee Spice", sans-serif;
  font-weight: 400;
  font-style: normal;
}
</style>
