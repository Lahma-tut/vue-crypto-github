<script setup>
const props = defineProps({
  changeAmount: {
    type: Function,
    required: true
  },
  convert: {
    type: Function,
    required: true
  },
  favourite: {
    type: Function,
    required: true
  }
})
</script>

<template>
  <input 
    type="number" 
    min="0" 
    @input="changeAmount($event.target.value)" 
    placeholder="Введите число">

    <button @click="convert">Конвертировать</button>
    <button @click="favourite" class="btn-fav">В избранное</button>
</template>

<style scoped>
input {
  width: 360px;
  padding: 11px 25px;
  border-radius: 2px;
  border: 0;
  outline: none;
  color: #333;
  background: #f1f1f1;
  font-size: 1em;
  margin-right: 10px;
}

button {
  margin: 0 5px;
}

.btn-fav {
  
}

</style>
