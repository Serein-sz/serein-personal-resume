<script setup lang="ts">
import { ref } from 'vue';

interface ProjectExperience {
  name: string;
  time: string;
  role: string;
  description: string;
  techStack: string[];
  responsibilities: string[];
}

const projectExperiences = ref<ProjectExperience[]>([
  {
    name: '生产管理系统开发平台',
    time: '2023-07 - 至今',
    role: '全栈工程师',
    description: '0/低代码快速开发平台，提供组件拖拽式表单配置，快速开发业务表单，提供工作流能力',
    techStack: ['spring cloud', 'kubernetes', 'spring ai', 'redis', 'mysql', 'minio', 'rabbitmq', 'vue2'],
    responsibilities: [
      '0/低代码引擎架构设计',
      'Java在线编译器',
      '工作流程引擎开发',
      'MCP接入',
    ],
  },
  {
    name: '多维报表',
    time: '2024-01 - 至今',
    role: '全栈工程师',
    description: '复杂报表构建器',
    techStack: ['spring cloud', 'redis', 'mysql', 'minio', 'kubernetes', 'rabbitmq', 'vue3', 'tailwindcss'],
    responsibilities: [
      '复杂报表构建引擎设计开发',
      '函数解释执行器设计开发',
    ],
  },
]);
</script>

<template>
  <div class="project-experience-section">
    <div class="text-2xl font-semibold mb-2">项目经历</div>
    <div v-for="(project, index) in projectExperiences" :key="index" class="mb-6">
      <div class="text-xl font-semibold mb-1">{{ project.name }}</div>
      <div class="text-sm text-gray-600 dark:text-gray-400 mb-2">
        <span>{{ project.time }}</span> | <span>{{ project.role }}</span>
      </div>
      <p class="text-gray-700 dark:text-gray-300 mb-2" v-if="project.description">{{ project.description }}</p>
      <div class="mb-2">
        <div class="font-medium text-gray-800 dark:text-gray-200">核心技术栈:</div>
        <div class="flex flex-wrap gap-2 mt-1">
          <span v-for="(tech, techIndex) in project.techStack" :key="techIndex"
            class="px-2 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full dark:bg-blue-900 dark:text-blue-300">
            {{ tech }}
          </span>
        </div>
      </div>
      <div>
        <div class="font-medium text-gray-800 dark:text-gray-200">职责与贡献:</div>
        <ul class="list-disc list-inside ml-4 mt-1 space-y-1 text-gray-700 dark:text-gray-300">
          <div v-for="(resp, respIndex) in project.responsibilities" :key="respIndex" class="flex gap-2">
            <div class="flex items-center">
              <div class="w-1 h-1 rounded-full bg-black"></div>
            </div>
            <span>
              {{ resp }}
            </span>
          </div>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Add any additional scoped styles here if needed */
.project-experience-section {

  /* Example of responsive design: adjust padding for smaller screens */
  @media (max-width: 768px) {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
}
</style>