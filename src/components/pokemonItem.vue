<template>
  <div @click="$emit('showPokemonData', pokemon.id)">
    <img :src="pokemon.image">
    <p class="text text--25"> {{ pokemon.name }} </p>
  </div>
</template>

<script>
  // import axios from 'axios'

  export default {
    name: "pokemonItem",
    props: ["pokemon"],
  }
</script>
