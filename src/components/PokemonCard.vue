<template>
    <div :class="['card', `type-${pokemon.type}`]" @click="goToDetails">
      <img :src="pokemon.photo" :alt="pokemon.name" />
      <h2 class="pokemon-name">{{ pokemon.name.toUpperCase() }}</h2>
      <p>Peso: {{pokemon.weight}} kg</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PokemonCard',
    props: {
      pokemon: Object
    },
    methods: {
      goToDetails() {
        this.$router.push(`/pokemon/${this.pokemon.id}`);
      }
   
    }
  };
  </script>

  