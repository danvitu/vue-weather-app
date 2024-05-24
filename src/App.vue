<script setup>
import SiteNavigation from './components/SiteNavigation.vue';
</script>

<template>
  <div class="flex flex-col min-h-screen font-Roboto bg-weather-primary">
    <SiteNavigation></SiteNavigation>
    <RouterView />
  </div>
</template>

<style scoped></style>
