<script setup lang="ts">
import { useColorMode } from '@vueuse/core';
import GalaxyBackground from './components/GalaxyBackground.vue';
const mode = useColorMode()
mode.value = 'light'
</script>

<template>
  <RouterView />
  <!-- <div class="relative flex items-center justify-center h-screen">
    <GalaxyBackground />
    <RouterView class="absolute top-1/2 left-1/2 min-h-[80vh] w-[80vw] transform -translate-x-1/2 -translate-y-1/2" />
  </div> -->
</template>

<style scoped>
</style>
