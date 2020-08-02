<template>
  <div class="container">
    <div class="web-loader">
      <img class="pokeball" src="./img/pokeball-dark.png" alt="pokeball">
      <p class="text text--20"> catching pokemons... </p>
    </div>
    <pokemonData :pokemonData="pokemonData" />
    <pokemonSearch :pokemons="pokemons" v-on:filterData="filterData" />
    <pokemonList :pokemons="pokemons" v-on:showPokemonData="showPokemonData" />
  </div>
</template>

<script>
import pokemonData from './components/pokemonData'
import pokemonSearch from './components/pokemonSearch'
import pokemonList from './components/pokemonList'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    pokemonList,
    pokemonSearch,
    pokemonData
  },
  data() {
    return {
      pokemons: [],
      pokemonsBackup: [],
      pokemonData: []
    }
  },
  methods: {
    getPokemons(pokemonCount) {
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${pokemonCount}/`)
        .then(
          res => {
            // declare new pokemon (object type)
            let pokemon = res.data
            let pokemonAbilities = pokemon.abilities

            let newPokemon = {
              id: pokemonCount,
              name: pokemon.name,
              type: pokemon.types[0].type.name,
              abilitiesURL: [],
              abilities: [],
              image: pokemon.sprites.front_default
            }

            // push URL abilities to newPokemon (idk y i pushed it but maybe we'll need it)

            for(let pokemonAbility of pokemonAbilities) {
              newPokemon.abilitiesURL.push(pokemonAbility.ability.url)
            }

            // get ablities based from ability URL 
            let pokemonAbilitiesURL = newPokemon.abilitiesURL

            for(let pokemonAbilityURL of pokemonAbilitiesURL) {
              axios
                .get(pokemonAbilityURL)
                .then(
                  res => {
                    let abilityName = res.data.name
                    let abilityDes = res.data.effect_entries[1].effect || 'none'
                    let newAbility = {
                      abilityName: abilityName,
                      abilityDes: abilityDes
                    }
                    newPokemon.abilities.push(newAbility)
                  }
                )
                .catch(err => console.log(err))
            }

            // push it to pokemons array
            this.pokemons.push(newPokemon)
            this.pokemonsBackup.push(newPokemon)
          }
        )
        .catch(err => console.log(err))
        .finally(
          res => {
            if(res != undefined || res !=null)
              console.table(res)
            if(pokemonCount == 806) {
              const webLoader = document.querySelector('.web-loader')
              webLoader.classList.add('web-loader--done')
            }
          }
        )
    },
    showPokemonData(id) {
      const pokemonData = this.pokemons.filter(
        pokemon => pokemon.id == id
      )
      this.pokemonData = pokemonData[0]

      const dataHolder = document.querySelector('.pokemon-data-holder')
      dataHolder.classList.add('pokemon-data-holder--active')

      const searchBar = document.querySelector('.left-panel')
      searchBar.classList.add('left-panel--hide')

      const body = document.querySelector('body')
      body.classList.add('overflowHidden')
    },
    filterData(filterData){
      this.pokemons = this.pokemonsBackup.filter(
        pokemon => pokemon.name.includes(filterData)
      )
    }
  },
  created() {
    for (let i = 1; i < 807; i++) {
      this.getPokemons(i)
    }
  },
}
</script>

<style lang="scss">

  /* reset css */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  }

  html,
  body {
    width: 100%;
    font-size: 10px;
  }

  ul {
    list-style-type: none;
  }

  a {
    text-decoration: none;
  }

  /* end of rest css */

  /* imports */

  @import './scss/main.scss'

</style>
