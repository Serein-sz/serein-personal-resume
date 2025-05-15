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

/**
 * 项目经历数据
 * @author 王强
 * @date 2025-05-06
 * @version 1.0.0
 */
const projectExperiences = ref<ProjectExperience[]>([
  {
    name: '生产管理系统开发平台',
    time: '2023-07 - 至今',
    role: '全栈工程师',
    description: '基于微服务架构的企业级0/低代码快速开发平台，采用可视化拖拽式组件配置，实现业务表单的快速构建与部署。平台集成了自定义工作流引擎，支持复杂业务流程的灵活配置与自动化执行，显著提升了企业生产管理效率与系统开发速度，降低了技术门槛与维护成本。',
    techStack: ['spring cloud', 'kubernetes', 'spring ai', 'redis', 'mysql', 'rabbitmq'],
    responsibilities: [
      '设计并实现基于DSL的0/低代码引擎核心架构，支持组件级别的元数据定义与解析',
      '开发高性能Java动态编译与热加载系统，实现业务代码的实时编译与执行',
      '构建基于BPMN2.0规范的工作流引擎，支持自定义节点与条件分支逻辑',
      '设计实现MCP协议接入层',
    ],
  },
  {
    name: '多维报表',
    time: '2024-01 - 至今',
    role: '全栈工程师',
    description: '企业级多维数据分析与可视化平台，支持复杂数据源的动态接入与实时计算。系统提供丰富的图表组件与交互式数据透视功能，实现了数据可视化展示的全流程解决方案。平台采用微服务架构设计，具备高并发处理能力与横向扩展特性，满足大规模企业数据分析需求。',
    techStack: ['spring cloud', 'kubernetes', 'redis', 'mysql', 'mongodb', 'rabbitmq'],
    responsibilities: [
      '设计并实现的报表构建引擎，支持复杂数据模型定义与数据计算',
      '开发基于AST的高性能函数解释执行器，实现自定义公式的动态计算与实时渲染',
      '设计并实现多异构数据源聚合引擎，支持关系型数据库(MySQL)、NoSQL(MongoDB)、时序数据库等多种数据源的统一接入与查询；通过分布式缓存与预计算机制优化查询性能，将复杂聚合查询响应时间控制在300毫秒左右',
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
