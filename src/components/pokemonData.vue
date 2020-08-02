<template>
  <div class="pokemon-data-holder" v-on:click="hideData">
    <ul class="pokemon-data-container">
      <li class="pokemon-data-image-container">
        <img class="pokemon-data-image" src="../img/pokeballUpper.png" alt="PokeBall Upper">
        <img class="pokemon-data-image-main" :src="pokemonData.image">
        <img class="pokemon-data-image pokemon-data-image--bottom" src="../img/pokeballLower.png" alt="PokeBall Upper">
      </li>
      <li class="pokemon-data">
        <h2 class="pokemon-data__title"> POKEMON DATA </h2>
        <div class="pokemon-data-row pokemon-data-row--name">
          <p class="pokemon-data__label"> [ Pokemon ] - </p>
          <p class="pokemon-data__info">
            <vue-typer
              :repeat='0'
              :text='pokemonData.name || "null" '>
            </vue-typer>
          </p>
        </div>

        <div class="pokemon-data-row">
          <p class="pokemon-data__label"> [ Type ] - </p>
          <p class="pokemon-data__info">
            <vue-typer
              :repeat='0'
              :text='pokemonData.type || "null" '>
            </vue-typer>
          </p>
        </div>

        <h3 class="pokemon-data__subtitle"> Pokemon Abilities </h3>

        <div class="pokemon-data-ability" v-for="(ability, i) in pokemonData.abilities" :key="i">
          <h4 class="pokemon-data__label pokemon-data__label--mb25"> {{ ability.abilityName }} </h4>
          <p class="pokemon-data__info">
            <vue-typer
              type-delay='1'
              :repeat='0'
              :text='ability.abilityDes || "null" '>
            </vue-typer>
          </p>
        </div>

      </li>
    </ul>
  </div>
</template>

<script>
  import { VueTyper } from 'vue-typer'

  export default {
    name: "pokemonData",
    props: ["pokemonData"],
    components: {
      VueTyper
    },
    methods: {
      hideData() {
        const dataHolder = document.querySelector('.pokemon-data-holder')
        dataHolder.classList.remove('pokemon-data-holder--active')
        const body = document.querySelector('body')
        body.classList.remove('overflowHidden')
      }
    },
  }
</script>