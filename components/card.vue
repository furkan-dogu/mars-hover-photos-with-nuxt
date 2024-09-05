<template>
    <div  
        v-for="item in filteredData"
        :key="item.id"
        class="font-medium flex flex-col gap-1"
    >
        <img :src="item.img_src" :alt="item.id" class="w-[300px] h-72 rounded-lg shadow-sm shadow-white hover:shadow-md hover:shadow-white">
        <p>Date: {{ item.earth_date }}</p>
        <p>Camera: {{ item.camera.full_name }}</p>
    </div>
</template>

<script setup>
const props = defineProps(["filteredData"])
</script>