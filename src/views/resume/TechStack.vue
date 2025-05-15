<script setup lang="ts">
import { ref } from 'vue';

const techStack = ref([
  { id: 1, description: '熟练使用Java、JavaScript、Golang、Python等语言' },
  { id: 2, description: '熟练使用spring cloud、vue、react等前后端框架' },
  // Add more tech stack items here if needed
]);
</script>

<template>
  <div>
    <div class="text-2xl font-semibold mb-2">
      技术栈
    </div>
    <div>
      <div v-for="tech in techStack" :key="tech.id" class="flex gap-2">
        <div class="flex items-center">
          <div class="w-1 h-1 rounded-full bg-black"></div>
        </div>
        <span>
          {{ tech.description }}
        </span>
      </div>
    </div>
  </div>
</template>