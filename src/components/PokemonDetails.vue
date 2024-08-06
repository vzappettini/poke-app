<template>
    <div :class="['pokemon-detail', `type-${pokemon.type}`]">
      <h1 class="pokemon-name">{{ pokemon.name.toUpperCase() }}</h1>
      <img :src="pokemon.photo" :alt="pokemon.name" class="pokemon-photo" />
      <div class="pokemon-info">
        <p><strong>Tipo:</strong> {{ pokemon.type }}</p>
        <p><strong>Peso:</strong> {{ pokemon.weight }} kg</p>
        <p v-if="pokemon.description"><strong>Descripción:</strong> {{ pokemon.description }}</p>
      </div>
      <h2 class="moves-title">Movimientos</h2>
      <ul class="moves-list">
        <li v-for="move in pokemon.moves" :key="move" class="move">{{ move }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      pokemon: Object
    },
    
    }
  </script>
  

  