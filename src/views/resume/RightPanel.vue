<script setup lang="ts">
import Separator from '@/components/ui/separator/Separator.vue';
import TechStack from './TechStack.vue';
import WorkExperienceSection from './WorkExperienceSection.vue';
import ProjectExperienceSection from './ProjectExperienceSection.vue';
</script>
<template>
    <div class="p-6 pt-1">
        <TechStack />
        <Separator class="my-2" />
        <WorkExperienceSection />
        <Separator class="my-2" />
        <ProjectExperienceSection />
    </div>
</template>