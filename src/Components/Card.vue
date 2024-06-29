<template>
    <div class="flex flex-col overflow-hidden rounded-xl shadow-xl">
      <div>
        <img v-if="props.character" :src="`https://jojos-bizarre-api.netlify.app/assets/${props.character.image}`" alt="image" width="200" height="350"/>
      </div>
      <div>
        <h3>{{ props.character.name }}</h3>
      </div>
    </div>
</template>

<script setup>
const props = defineProps({
  character: {
    required: true,
    type: Object
  }
})
</script>
