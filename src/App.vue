<script setup>
import CardPersonnage from './components/CardPersonnage.vue';
import { ref } from 'vue';
import { onMounted } from 'vue';

const characters = ref([]);
const page = ref(1);

async function getCharacters() {
  const response = await fetch('https://rickandmortyapi.com/api/character?page=' + page.value);
  const data = await response.json();
  characters.value = data.results;
}

onMounted(() => {
  getCharacters();
});

function nextPage() {
  page.value = page.value + 1;
  getCharacters();

  // Scroll de la page vers le haut
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
}

function previousPage() {
  page.value = page.value - 1;
  getCharacters();

  // Scroll de la page vers le haut
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
}

</script>
<template>
  <main v-if="characters">
    <header class=" flex items-center justify-center m-8">
      <img src="/image.png" class="w-64">
    </header>
    <main class="grid gap-2 grid-cols-1 lg:grid-cols-8 md:grid-cols-3 sm:grid-cols-2 m-2">
      <CardPersonnage v-for="character in characters" :key="character.id" :name="character.name"
        :image="character.image" :status="character.status" />
    </main>

    <div class="flex flex-row items-center justify-center justify-around">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="previousPage()"
        v-if="page != 1">Page précédente</button>
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="nextPage()">Page
        suivante</button>
    </div>
  </main>

</template>