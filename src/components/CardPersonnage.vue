<script setup>
import { onMounted, ref } from 'vue';

const character = defineProps({
    name: String,
    image: String,
    status: String,
});

</script>

<template>
    <div class="flex flex-col bg-white p-2 rounded-lg items-center" v-if="character">
        <img :src="character.image" class="w-64 rounded-sm">
        <h1 class="text-xl text-black mt-2">{{ character.name}}</h1>
        <h1 class="text-lg text-black" v-if="die">Décédé</h1>
        <h1 class="text-lg text-black" v-else>Vivant</h1>
    </div>
</template>