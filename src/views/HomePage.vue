<template>
    <div class="home-page">
      <h1 class="page-title">Pokémones</h1>
      <div class="cards-container">
        <PokemonSection type="fire" />
      <PokemonSection type="water" />
      <PokemonSection type="grass" />
      <PokemonSection type="electric" />
      <PokemonSection type="flying" />
      <PokemonSection type="psychic" />
      <PokemonSection type="fighting" />
      <PokemonSection type="bug" />
      <PokemonSection type="rock" />
      <PokemonSection type="ghost" />
      <PokemonSection type="dragon" />
      <PokemonSection type="dark" />
      <PokemonSection type="steel" />
      <PokemonSection type="fairy" />
      </div>
    </div>
  </template>
  
  <script>
  import PokemonSection from '../components/PokemonSection.vue';
  
  export default {
    name: 'HomePage',
    components: {
      PokemonSection
    }
  };
  </script>
  
  <style>
  .home-page {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.page-title {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #333;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

@media (max-width: 768px) {
  .cards-container {
    flex-direction: column;
    align-items: center;
  }
}
  </style>