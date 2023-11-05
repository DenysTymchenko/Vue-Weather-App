<script setup>
const props = defineProps({
  weather: Object
})
</script>

<template>
  <div class='info' v-if='weather.location'>
    <h2>{{ weather.location }}</h2>
    <h3>{{ weather.date }}</h3>
    <h1>{{ weather.temperature }}°</h1>
    <h2>{{ weather.type }}</h2>
  </div>
</template>

<style scoped>
.info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.info h1 {
  width: 200px;
  background: rgb(241 241 241 / 50%);
  font-size: 3rem;
  padding: 40px;
  border-radius: 5px 20px;
  margin-bottom: 15px;
  box-shadow: 5px 5px 20px 2px rgba(0, 0, 0, 0.35);
}

.info h2 {
  font-size: 2rem;
}

.info h3 {
  font-size: 1rem;
  margin-bottom: 10px;
}
</style>
