<script setup>
import {computed, onMounted, reactive, ref} from "vue";
import ListPokemons from "@/components/ListPokemons.vue";
import CardPokemonSelected from "@/components/CardPokemonSelected.vue";
import axios from "axios";
import {initFlowbite} from "flowbite";

let urlPokemonList = ref("https://raw.githubusercontent.com/Biuni/PokemonGO-Pokedex/master/pokedex.json");
let pokemons = reactive(ref());
let searchPokemon = ref("");
let pokemonSelected = reactive(ref());

onMounted(() => {
  initFlowbite();
  axios.get(urlPokemonList.value)
      .then(res => pokemons.value = res.data.pokemon);
})

const pokemonsFiltered = computed(() => {
  if (pokemons.value && searchPokemon.value) {
    return pokemons.value.filter(
        pokemon => pokemon.name.toLowerCase().includes(searchPokemon.value.toLowerCase())
    )
  }
  return pokemons.value;
})

const selectPokemon = (pokemon) => {
  pokemonSelected.value = pokemon;
}
</script>

<template>
  <main>
    <div class="grid gap-4 grid-cols-1 md:grid-cols-2">
      <div class="w-50 text-center">
          <CardPokemonSelected
              :name="pokemonSelected?.name"
              :id="pokemonSelected?.num"
              :image="pokemonSelected?.img"
              :height="pokemonSelected?.height"
              :weight="pokemonSelected?.weight"
              :types="pokemonSelected?.type"
              :weaknesses="pokemonSelected?.weaknesses"
          ></CardPokemonSelected>
      </div>
      <div class="w-50">
          <div class="card-list">
            <div class="">
              <div class="">
                <label for="searchPokemon" class="mb-2 text-sm font-medium text-slate-900 sr-only dark:text-white">Search</label>
                <div class="relative">
                  <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                    <svg aria-hidden="true" class="w-5 h-5 text-slate-500 dark:text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                    </svg>
                  </div>
                  <input v-model="searchPokemon" type="search" id="searchPokemon" class="block w-full p-4 pl-10 text-sm text-slate-900 border border-slate-300 rounded-lg bg-slate-50 focus:ring-purple-500 focus:border-purple-500 dark:bg-slate-700 dark:border-slate-600 dark:placeholder-slate-400 dark:text-white dark:focus:ring-purple-500 dark:focus:border-purple-500" placeholder="Pokemon" required>
                </div>
              </div>
              <div class="grid grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 place-content-center">
              <ListPokemons
                  v-for="pokemon in pokemonsFiltered"
                  :key="pokemon.name"
                  :name="pokemon.name"
                  :image="pokemon.img"
                  :type="pokemon.type[0].toLowerCase()"
                  @click="selectPokemon(pokemon)">
              </ListPokemons>
              </div>
            </div>
          </div>
        </div>
      </div>
  </main>
</template>

<style scoped>
.card-list {
  overflow-y: scroll;
  height: 75vh;
  overflow-x: hidden;;
}
</style>
