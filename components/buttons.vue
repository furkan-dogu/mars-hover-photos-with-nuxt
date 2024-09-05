<template>
    <div class="flex justify-center items-center flex-wrap gap-2.5 px-2.5">
        <button 
            class="w-32 font-medium bg-gray-500 border-none outline-none h-7 rounded-lg tracking-wider hover:shadow-md hover:shadow-white"
            v-for="camera in cameras"
            :key="camera"
            @click="handleClick(camera)"
        >
            {{ camera }}
        </button>
    </div>
</template>

<script setup>
const props = defineProps(["filteredData", "info", "cameraName"])
const emit = defineEmits(["update:cameraName", "update:filteredData"])

const cameras = ["ALL", "FHAZ", "NAVCAM", "MAST", "CHEMCAM", "RHAZ"]

const filteredCamera = (camera) => {
    if (camera === "ALL") {
        emit("update:filteredData", props.info)
    } else {
        const filtered = props.info.filter(item => item.camera.name === camera)
        emit("update:filteredData", filtered)
    }
}

const handleClick = (camera) => {
    filteredCamera(camera)
    emit("update:cameraName", camera)
}
</script>