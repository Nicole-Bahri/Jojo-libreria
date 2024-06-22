<script setup>
import { ref } from 'vue'
import Card from '@/Components/Card.vue';
import router from '@/router'
let character = ref([])
let page = ref(1)

function nextPage() {
  page.value++
  loadCharacters()
}

function previousPage() {
  page.value--
  if (page.value < 1) {
    page.value = 1
  }
  loadCharacters()
}

async function loadCharacters() {
  const response = await fetch(`https://stand-by-me.herokuapp.com/api/v1/characters?page=${page.value}`)
  const data = await response.json()
  character.value = data
  console.log(data)
  console.log(character.value)
}
loadCharacters()
</script>

<template>
  <div class="flex justify-center mb:12 mt-10">
    <h1 class="text-3xl md:text-5xl">Personajes de Jojo's</h1>
  </div>

  <div class="flex justify-center items-center m-4 space-x-4">
    <button
      class="bg-gray-300 rounded-xl text-center p-4"
      @click="previousPage"
      :disabled="page === 1"
    >
      < Pagina anterior
    </button>
    <div>{{ page }}</div>
    <button class="bg-gray-300 rounded-xl text-center p-4" @click="nextPage">
      Siguiente pagina >
    </button>
  </div>
  <div class="grid gap-4 grid-cols-2 md:grid-cols-3 lg:grid-cols-5 m-6">
    <router-link v-for="personajes in character" :key="personajes.id" :to="`/${personajes.id}`">
      <Card :character="personajes"></Card>
    </router-link>
  </div>
</template> 