<script setup>
import { ref } from 'vue';
import SearchBar from './components/SearchBar.vue';
import WeatherInfo from './components/WeatherInfo.vue';

const apiKey = '90fc3238cca00624e8144eeb9883fb27';
const urlBase = 'https://api.openweathermap.org/data/2.5/weather';
const weather = ref({
  location: null,
  date: null,
  temperature: null,
  type: null,
});
const rainyWeather = ['Rain', 'Snow', 'Drizzle'];
const foggyWeather = ['Fog', 'Mist', 'Haze', 'Smoke'];
const dangerWeather = ['Thunderstorm', 'Tornado'];
const appClass = ref(null)

const getCurrentDate = () => {
  const date = new Date()
  const options = { weekday: 'long', day: 'numeric', month: 'long', year: 'numeric' };
  return date.toLocaleDateString('en-US', options);
}
const changeAppColors = () => {
  const app = document.getElementById('app')
  const weatherType = weather.value.type;

  app.className = ''

  if (rainyWeather.includes(weatherType)) app.classList.add('rainy')
  else if (foggyWeather.includes(weatherType)) app.classList.add('foggy');
  else if (dangerWeather.includes(weatherType)) app.classList.add('danger');
  else app.classList.add(weatherType.toLowerCase())


}
const fetchWeather = (query) => {
  fetch(`${urlBase}?units=metric&q=${query}&appid=${apiKey}`)
      .then((response) => response.json())
      .then((data) => setWeatherData(data))
      .catch((error) => console.error(error));
}
const setWeatherData = (data) => {
  weather.value = {
    location: `${data.name}, ${data.sys.country}`,
    date: getCurrentDate(),
    temperature: Math.round(data.main.temp),
    type: data.weather[0].main,
  }

  changeAppColors()
}
</script>

<template>
  <search-bar @fetchWeather='(query) => fetchWeather(query)' />
  <weather-info :weather='weather'></weather-info>
</template>
