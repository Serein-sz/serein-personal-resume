<script setup lang="ts">
import { ref } from 'vue';

interface WorkExperience {
    company: string;
    position: string;
    duration: string;
}

const workExperiences = ref<WorkExperience[]>([
    {
        company: '沈阳夸克智能科技有限公司',
        position: '全栈开发工程师',
        duration: '2023.07-至今(全职)',
    },
    {
        company: '联信弘方科技有限公司',
        position: 'Java开发工程师',
        duration: '2023.03-2023.6(实习)',
    },
]);
</script>

<template>
    <div>
        <div class="text-2xl font-semibold mb-2">
            工作经历
        </div>
        <div>
            <div v-for="(experience, index) in workExperiences" :key="index" class="flex justify-between mb-2">
                <div class="font-bold">
                    {{ experience.company }}
                </div>
                <div class="flex">
                    <div class="mr-2">
                        {{ experience.position }}
                    </div>
                    <div class="w-42">
                        {{ experience.duration }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>