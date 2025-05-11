<script setup lang="ts">
const props = defineProps<{
    infos: string[];
}>()
</script>
<template>
    <div>
        <div v-for="info in infos" class="text-gray-300">{{ info }}</div>
    </div>
</template>