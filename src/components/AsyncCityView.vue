<script setup>
import axios from 'axios'
import { useRoute } from 'vue-router'

const WEATHER_API_API = 'f6a31bc29e5349c896785531242502'

const route = useRoute()
const getWeatherData = async () => {
  try {
    const weatherData = await axios.get(
      `http://api.weatherapi.com/v1/forecast.json?key=${WEATHER_API_API}&q=${route.query.lat},${route.query.lng}&days=7&lang=ru`
    )
    await new Promise((res) => setTimeout(res, 500))
    return weatherData.data
  } catch (err) {
    console.log(err)
  }
}
const weatherData = await getWeatherData()
console.log(weatherData)
</script>

<template>
  <div class="flex flex-col flex-1 items-center">
    <!-- Banner -->
    <!-- <div v-if="route.query.preview" class="text-white p-4 bg-weather-secondary w-full text-center">
      <p>Вы смотрите прогноз в этом городе</p>
    </div> -->
    <!-- Weather Overview -->
    <div class="flex flex-col items-center text-white py-12">
      <h1 class="text-4xl mb-2">{{ route.params.city }}</h1>
      <p class="text-sm mb-12">
        {{
          new Date(weatherData.location.localtime).toLocaleDateString('ru-RU', {
            weekday: 'long',
            day: '2-digit',
            month: 'long'
          })
        }}
        {{
          new Date(weatherData.location.localtime).toLocaleTimeString('ru-RU', {
            hour: '2-digit',
            minute: '2-digit'
          })
        }}
      </p>
      <p class="text-8xl mb-8">{{ Math.round(weatherData.current.temp_c) }}&deg;</p>
      <p>
        Ощущается, как
        {{ Math.round(weatherData.current.feelslike_c) }} &deg;
      </p>
      <p class="capitalize">
        {{ weatherData.current.condition.text }}
      </p>
      <img class="h-auto" :src="weatherData.current.condition.icon" alt="Weather Icon" />
    </div>

    <hr class="border-white border-opacity-10 border w-full" />

    <!-- Hourly Weather -->
    <div class="max-w-screen-md w-full py-12">
      <div class="mx-8 text-white">
        <h2 class="mb-4">Почасовой прогноз</h2>
        <div class="flex gap-10 overflow-x-scroll">
          <div
            v-for="hourData in weatherData.forecast.forecastday[0].hour"
            :key="hourData"
            class="flex flex-col gap-4 items-center"
          >
            <p class="whitespace-nowrap text-md">
              {{
                new Date(hourData.time).toLocaleTimeString('ru-RU', {
                  hour: '2-digit',
                  minute: '2-digit'
                })
              }}
            </p>
            <img
              class="h-12 min-w-min object-cover"
              :src="hourData.condition.icon"
              alt="Hourly Weather Icon"
            />
            <p class="text-xl">{{ Math.round(hourData.temp_c) }}&deg;</p>
          </div>
        </div>
      </div>
    </div>

    <hr class="border-white border-opacity-10 border w-full" />

    <!-- Weekly Weather -->
    <div class="max-w-screen-md w-full py-12">
      <div class="mx-8 text-white">
        <h2 class="mb-4">Прогноз на ближайшие дни</h2>
        <div v-for="day in weatherData.forecast.forecastday" :key="day" class="flex items-center">
          <p class="flex-1">
            {{
              new Date(day.date).toLocaleDateString('ru-RU', {
                weekday: 'long',
                day: '2-digit',
                month: 'short'
              })
            }}
          </p>
          <img class="w-[50px] h-[50px] object-cover" :src="day.day.condition.icon" alt="" />
          <div class="flex gap-2 flex-1 justify-end">
            <p>Max: {{ Math.round(day.day.maxtemp_c) }}</p>
            <p>Min: {{ Math.round(day.day.mintemp_c) }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
