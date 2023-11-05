<script setup>
import { ref } from 'vue';

const emit = defineEmits(['fetchWeather'])
const query = ref('')

</script>

<template>
  <form @submit.prevent="emit('fetchWeather', query)" class='search-bar'>
    <input type='text' placeholder='Search...' v-model='query'>
  </form>
</template>

<style scoped>
form {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-bottom: 20px;
}

form input {
  width: 50%;
  background-color: rgba(255, 255, 255, 0.5);
  padding: 20px;
  border: none;
  border-radius: 20px;
  box-shadow: 0 0 10px 3px rgba(0,0,0,0.35);
}
</style>
