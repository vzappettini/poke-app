<template>
    <div>
      <div v-if="paginatedPokemons.length > 0">
        <h2>Tipo de Pokémon: {{ type }}</h2>
        <div class="pokemon-list">
          <PokemonCard
            v-for="pokemon in paginatedPokemons[currentPage]"
            :key="pokemon.id"
            :pokemon="pokemon"
          />
        </div>
        <div class="pagination-controls">
          <button @click="prevPage" :disabled="currentPage === 0">&laquo;</button>
          <span>{{ currentPage + 1 }} de {{ totalPages }}</span>
          <button @click="nextPage" :disabled="currentPage === totalPages - 1">&raquo;</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import PokemonCard from './PokemonCard.vue';
  
  export default {
    components: {
      PokemonCard
    },
    props: {
      type: {
        type: String,
        required: true
      }
    },
    data() {
      return {
        pokemons: [],
        itemsPerPage: 4,
        currentPage: 0
      };
    },
    computed: {
      paginatedPokemons() {
        const result = [];
        for (let i = 0; i < this.pokemons.length; i += this.itemsPerPage) {
          result.push(this.pokemons.slice(i, i + this.itemsPerPage));
        }
        return result;
      },
      totalPages() {
        return this.paginatedPokemons.length;
      }
    },
    methods: {
      async fetchPokemonsByType(type) {
        try {
          // Primero, obtenemos los Pokémon por tipo
          const response = await fetch(`https://pokeapi.co/api/v2/type/${type}/`);
          const data = await response.json();
          
          // Extraemos las URLs de los Pokémon
          const pokemonUrls = data.pokemon.map(p => p.pokemon.url);
          
          // Obtenemos los detalles de cada Pokémon
          const pokemonDetailsPromises = pokemonUrls.map(url => fetch(url).then(res => res.json()));
          const pokemonDetails = await Promise.all(pokemonDetailsPromises);
          
          // Mapeamos los detalles a la estructura que usamos
          this.pokemons = pokemonDetails.map(pokemon => ({
            id: pokemon.id,
            name: pokemon.name,
            type: type,
            photo: pokemon.sprites.front_default,
            weight: pokemon.weight/10  
          }));
        } catch (error) {
          console.error('Error encontrando Pokémon:', error);
        }
      },
      prevPage() {
        if (this.currentPage > 0) {
          this.currentPage--;
        }
      },
      nextPage() {
        if (this.currentPage < this.totalPages - 1) {
          this.currentPage++;
        }
      }
    },
    async created() {
      await this.fetchPokemonsByType(this.type);
    }
  };
  </script>

  