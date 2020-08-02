<template>
  <div class="card-container">
    <ul class="card-list">
      <!-- eslint-disable vue/no-use-v-if-with-v-for,vue/no-confusing-v-for-v-if -->
      <li class="card" v-if="i < showList" v-for="(pokemon, i) in pokemons" :key="i"> 
        <pokemonItem :pokemon="pokemon" v-on:showPokemonData="$emit('showPokemonData', pokemon.id)" />
      </li>
    </ul>
    <div class="load-more" v-if="pokemons.length > 8" v-on:click="showList += 16"> LOAD MORE </div>
  </div>
</template>

<script>
  import pokemonItem from './pokemonItem'

  export default {
    name: "pokemonList",
    data() {
      return {
        showList: 8
      }
    },
    components: {
      pokemonItem
    },
    props: ["pokemons"],
  }
</script>

<style scoped>

</style>