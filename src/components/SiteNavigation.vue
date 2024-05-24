<script setup>
import BaseModal from './BaseModal.vue'
import { ref } from 'vue'

const modalActive = ref(null)
const toggleModal = () => {
  modalActive.value = !modalActive.value
}
</script>

<template>
  <header class="sticky top-0 bg-weather-primary shadow-lg">
    <nav class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6">
      <RouterLink :to="{ name: 'home' }">
        <div class="flex items-center gap-3">
          <i class="fa-solid fa-sun text-2xl"></i>
          <p class="text-2xl">Прогноз погоды</p>
        </div>
      </RouterLink>
      <div class="flex gap-3 flex-1 justify-end">
        <i
          @click="toggleModal"
          class="fa-solid fa-circle-info text-xl hover:text-weather-secondary duration-150 cursor-pointer"
        ></i>
        <!-- <i
          class="fa-solid fa-plus text-xl hover:text-weather-secondary duration-150 cursor-pointer"
        ></i> -->
      </div>

      <BaseModal :modalActive="modalActive" @close-modal="toggleModal">
        <div class="text-black">
          <h1 class="text-2xl mb-1">О программе:</h1>
          <p class="mb-4">
            Прогноз погоды позволяет узнать текущую и будущую погоду в выбранных вами городах
          </p>
          <h2 class="text-2xl">Как это работает:</h2>
          <ol class="list-decimal list-inside mb-4">
            <li>Найдите свой город, введя его название в строку поиска.</li>
            <li>
              Выберите город в результатах поиска, и вы увидите текущую погоду для выбранного вами
              города.
            </li>
          </ol>
        </div></BaseModal
      >
    </nav>
  </header>
</template>
