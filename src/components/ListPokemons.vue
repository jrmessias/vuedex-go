<script setup>
const pokemon = defineProps(["name", "image", "type"])
</script>

<template>
  <div class="pokemon" :class="type">
    <p class="pokemon-title">
      {{ name.charAt(0).toUpperCase() + name.slice(1) }}
    </p>
    <img class="p-1 mx-auto transition duration-300 ease-in-out hover:-translate-y-1" :src="image" :alt="name" height="80">
  </div>
</template>

<style>
</style>
