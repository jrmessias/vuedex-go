<script setup>
const pokemon = defineProps(["id", "name", "image", "height",  "weight", "types", "weaknesses"])
</script>

<template>
  <div class="card-pokemon pokemon" :class="pokemon.types ? pokemon.types[0].toLowerCase() : '' ">
    <div class="flex justify-center" v-if="pokemon.image">
      <img :src="pokemon.image" class="p-4" height="300" :alt="pokemon.name">
      <img :src="pokemon.image.replace('pokemon/', 'pokemon/shiny/')" class="p-4" height="300" :alt="pokemon.name">✨
    </div>
    <div class="flex justify-center" v-else="pokemon.image">
      <img src="../assets/egg.svg" class="p-4" height="300" alt="">
    </div>
    <div class="w-100 py-4">
      <h5 class="font-bold text-2xl">{{ pokemon.name ?? "???" }}</h5>
      <div class="grid grid-cols-2">
        <div class="col-span-2">
          <span class="font-medium">Pokedéx:</span>
          <span class="col"> #{{ pokemon.id }}</span>
        </div>
        <div class="">
          <span class="font-medium">Peso:</span>
          <span class="col"> {{ pokemon.weight }}</span>
        </div>
        <div class="">
          <span class="font-medium">Altura:</span>
          <span class="col"> {{ pokemon.height }}</span>
        </div>
        <div class="">
          <span class="font-medium">Tipos:</span>
          <span class="col"> {{ pokemon.types ? pokemon.types.join(", ") : '' }}</span>
        </div>
        <div class="">
          <span class="font-medium">Fraquezas:</span>
          <span class="col"> {{ pokemon.weaknesses ? pokemon.weaknesses.join(", ") : '' }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
