<template>
    <div v-if="loading">
        <img src="@/assets/images/loading.gif" alt="Loading..." class="w-48 absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
    </div>
    <div v-else class="flex flex-col items-center">
        <h1 class="text-[40px] tracking-wider my-8 font-bold text-center">Mars Rover Photos</h1>
        <h3 class="text-2xl tracking-wider font-bold my-5">Cameras</h3>
        <Buttons 
            :info="info"
            v-model:filteredData="filteredData"
            v-model:cameraName="cameraName"
        />
        <h3 class="text-2xl tracking-wider font-bold my-5">{{ cameraName }} PHOTOS</h3>
        <div class="flex justify-center items-center flex-wrap gap-7 my-1 px-2.5">
            <Card :filteredData="filteredData" />
        </div>
    </div>
</template>

<script setup>
const config = useRuntimeConfig();
const API_KEY = config.public.apiKey

const info = ref(null)
const filteredData = ref([])
const loading = ref(false)
const cameraName = ref("ALL")

const getData = async () => {
    loading.value = true
    try {
        const res = await $fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=${API_KEY}`)
        info.value = res.photos
        filteredData.value = res.photos
    } catch (error) {
        console.log(error);
    } finally {
        loading.value = false
    }
}

onMounted(() => {
    getData()
})
</script>