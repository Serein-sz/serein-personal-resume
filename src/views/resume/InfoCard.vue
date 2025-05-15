<script setup lang="ts">
const props = defineProps<{
    infos: string[];
}>()
</script>
<template>
    <div>
        <span v-for="(info, index) in infos" class="text-xs">{{ info +  (index === infos.length - 1 ? "" : " | ")}}</span>
    </div>
</template>