<template>
  <div class="left-panel">
    <div class="logo-container">
      <img class="logo" src="../img/pokemonLogo.png" alt="P  okemon Logo">
      <p class="text text--20"> ULTIMATE POKEDEX </p>

      <input type="text" v-on:keyup="filterData">
    </div>
  </div>
</template>

<script>
  export default {
    name: "pokemonSearch",
    props: ["pokemons"],
    methods: {
      filterData() {
        let filterData = document.querySelector('input').value
        this.$emit('filterData', filterData)
      }
    },
  }
</script>

<style scoped>
  
</style>