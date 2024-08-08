<script setup>
const props = defineProps({
  favs: {
    type: Array,
    required: true
  },
  getFromFavs: {
    type: Function,
    required: true
  }
})
</script>

<template>
  <h2>Варианты в избранном</h2>
  <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<style scoped>
div {
  display: flex;
  justify-content: space-between;
  width: 500px;
  margin: 10px auto;
  transition: all 500ms ease;
}

span {
  padding: 10px 15px;
  background: #3cc2c0;

}

div:hover {
  opacity: 0.7;
  transform: scale(1.1);
  cursor: pointer;
}

</style>
