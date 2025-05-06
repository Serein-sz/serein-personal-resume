<script setup lang="ts">
import { renderGalaxy } from '@/lib/galaxy';
import { onMounted, useTemplateRef } from 'vue';

const galaxyRef = useTemplateRef('galaxy');

onMounted(() => {
  renderGalaxy(galaxyRef.value!);
})
</script>
<template>
  <div ref="galaxy" class="pointer-events-none w-full h-full"></div>
</template>
