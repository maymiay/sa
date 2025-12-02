<template>
  <form @submit.prevent="showResult" class="form">
    <input v-model="ip" />
    
    <select v-model="mask">
      <option v-for="option in options" :key="option" :value="option">
        {{ option }}
      </option>
    </select>

    <button type="submit" :disabled="!isIpValid(ip)">Рассчитать</button>
  </form>
  
  <div v-if="isShowResult && isIpValid(ip)" class="result"> 
    <div>IP: {{ ip }}</div>
    <div>Маска подсети: {{ mask }}</div>
    <div>Адрес сети: {{ getNetworkAdress(ip, mask) }}</div>
    <div>Количество адресов: {{ getAddressesCount(mask) }}</div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import { options } from './utils/options'
import { isIpValid, getNetworkAdress, getAddressesCount } from './utils/functions'

const ip = ref('')
const mask = ref(options[0]) 
const isShowResult = ref(false)

function showResult() {
  isShowResult.value = true
}
</script>

<style>
.form {
  display: flex;
  gap: 4px;
}

.result {
  border: 1px solid gray;
  border-radius: 16px;
  padding: 16px;
  margin-top: 32px;
  background-color: blue;
  color: white;
}
</style>