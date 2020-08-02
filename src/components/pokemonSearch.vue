<template>
  <div class="left-panel">
    <div class="logo-container">
      <img class="logo" src="../img/pokemonLogo.png" alt="P  okemon Logo">
      <p class="text text--20"> ULTIMATE POKEDEX </p>
    </div>

    <div class="search-sp">
      <p class="text text--25 text--yellow"> PokeSearch </p>
      <input class="pokemon-search" type="text" v-on:keyup="filterData">
    </div>

    <!-- <p class="text text--25 text--yellow"> PokeType </p> -->
    <p class="text text--20 text--mb20 text--intro"> 
      The Ultimate Pokedex is a Pokemon Collection Project Created for
      <span class="text--yellow">
        #PokeAddicts.
      </span> Click the PokeCard to view the Pokemon's Data.
    </p>

    <p class="text text--20 text--yellow sp-none"> TOOLS </p>

    <p class="text text--20 text--mb20 sp-none">
      <a class="text--white" target="_blank" href="https://vuejs.org/v2/guide/" >
        Vue JS 
      </a> and
      <a class="text--white" target="_blank" href="https://pokeapi.co/" >
        PokeAPI
      </a>
    </p>

    <p class="text text--20 text--yellow sp-none"> DEVELOPMENT </p>

    <a target="_blank" href="https://github.com/paoloLigsay/thepokemonproject" class="text text--20 sp-none">
      Github 
      <span class="text--yellow">
        [ thepokemonproject ] 
      </span> 
    </a>

    <a target="_blank" href="https://thecreativesdaily.com/paololigsay/" class="text text--20 sp-none">
      Developer
      <span class="text--yellow">
        [ Paolo Ligsay ] 
      </span> 
    </a>
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
    mounted() {
      const get = el => {
        let isMany = document.querySelectorAll(el).length > 1
        if (isMany) return document.querySelectorAll(el)
        return document.querySelector(el)
      }
      const body = document.querySelector('body')
      const logoCont = get('.logo-container')
      const logo = get('.logo')
      const intro = get('.text--intro')
      const searchSp = get('.search-sp')
      const leftPanel = get('.left-panel')

      body.onscroll = () => {
        if(window.pageYOffset > 200 && window.innerWidth <= 600) {
          logoCont.classList.add('logo-container--hide')
          logo.classList.add('logo--hide')
          intro.classList.add('text--intro-hide')
          searchSp.classList.add('search-sp--flex')
          leftPanel.classList.add('left-panel--fixed')
        } else {
          logoCont.classList.remove('logo-container--hide')
          logo.classList.remove('logo--hide')
          intro.classList.remove('text--intro-hide')
          searchSp.classList.remove('search-sp--flex')
          leftPanel.classList.remove('left-panel--fixed')
        }
      }
    },
  }
</script>

<style scoped>
  
</style>