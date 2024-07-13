<script setup>
import { ref } from 'vue'
import Card from '@/components/Card.vue';
import router from '@/router'
let character = ref([])
let page = ref({
  start: 0,
  end: 10
})

const actualCharacters = ref([])

async function loadCharacters() {
  const response = await fetch(
    `https://stand-by-me.herokuapp.com/api/v1/characters?page=${page.value}`
  )
  const data = await response.json()
  character.value = data
}

const changePage = () => {
  actualCharacters.value = character.value.slice(page.value.start, page.value.end)
  console.log(actualCharacters)
  page.value.start = page.value.start + 10
  page.value.end = page.value.end + 10

  console.log('start', page.value.start)
  console.log('end', page.value.end)
}

const previousPage = () => {
  actualCharacters.value = character.value.slice(page.value.start, page.value.end)
  console.log(actualCharacters)
  page.value.start = page.value.start - 10
  page.value.end = page.value.end - 10

  console.log('start', page.value.start)
  console.log('end', page.value.end)
}

loadCharacters()
</script>

<template>
  <div class="flex justify-center mb:12 mt-10">
    <h1 class="text-3xl md:text-5xl">Personajes de Jojo's</h1>
  </div>

  <div class="Y7eBOXZBuWX_SpAA0uHS" bis_skin_checked="1">
    <button @click="previousPage">-</button>
    <p>Si quieres volver, reinicia la pagina</p>
    <button @click="changePage">+</button>
  </div>
  <div class="grid gap-4 grid-cols-2 md:grid-cols-3 lg:grid-cols-5 m-6">
    <router-link
      v-for="personajes in actualCharacters"
      :key="personajes.id"
      :to="`/${personajes.id}`"
    >
      <Card :character="personajes"></Card>
    </router-link>
  </div>
</template>
