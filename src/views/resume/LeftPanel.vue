·<script setup lang="ts">
import { ref, computed } from 'vue';
import InfoCard from './InfoCard.vue';
import { Avatar, AvatarImage } from '@/components/ui/avatar';
import Image from '@/assets/image.jpg'
import Separator from '@/components/ui/separator/Separator.vue';

const workStartDate = '2023-07-06';

const calculateWorkExperience = (startDateString: string): string => {
    const start = new Date(startDateString);
    const today = new Date();

    let years = today.getFullYear() - start.getFullYear();
    let months = today.getMonth() - start.getMonth();

    if (months < 0 || (months === 0 && today.getDate() < start.getDate())) {
        years--;
        months += 12;
    }

    // Adjust months if the current day is earlier than the start day,
    // ensuring we count full months correctly.
    if (today.getDate() < start.getDate() && months > 0) {
        months--;
    }

    // User requirement: if months > 6, round up the year.
    if (months > 6) {
        years++;
    }

    if (years > 0) {
        return `${years}年经验`;
    } else {
        return '不足1年经验';
    }
};

const expectedPosition = computed<string[]>(() => [
    'Java开发工程师',
    '薪资面议',
    calculateWorkExperience(workStartDate),
    '在职状态',
]);

const birthDate = '2001-03-06';

const calculateAge = (birthDateString: string): number => {
    const birth = new Date(birthDateString);
    const today = new Date();
    let age = today.getFullYear() - birth.getFullYear();
    const m = today.getMonth() - birth.getMonth();
    if (m < 0 || (m === 0 && today.getDate() < birth.getDate())) {
        age--;
    }
    return age;
};

const baseInfo = computed<string[]>(() => [
    '王强',
    `${calculateAge(birthDate)}岁`,
    '本科',
    '中共党员',
    '13050795970',
    'q13050795970@163.com',
]);

const educationExperience = ref<string[]>([
    '防灾科技学院',
    '本科/数据科学与大数据技术',
    '2019.09-2023.06',
]);

</script>
<template>
    <div class="p-6">
        <Avatar class="h-36 w-36">
            <AvatarImage :src="Image" class="object-cover object-[center_-20px]" />
        </Avatar>
        <div class="mt-8">
            <div class="text-2xl mb-2">求职意向</div>
            <InfoCard :infos="expectedPosition" />
        </div>
        <Separator class="my-4" />
        <div>
            <div class="text-2xl mb-2">基本信息</div>
            <InfoCard :infos="baseInfo" />
        </div>
        <Separator class="my-4" />
        <div>
            <div class="text-2xl mb-2">教育经历</div>
            <InfoCard :infos="educationExperience" />
        </div>
    </div>
</template>