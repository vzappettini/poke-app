<template>
  <div class="pokemon-details">
    <PokemonDetails v-if="pokemon" :pokemon="pokemon" />
    <p v-else>Cargando...</p>
  </div>
</template>

<script>
import PokemonDetails from '@/components/PokemonDetails.vue';

export default {
  components: {
    PokemonDetails
  },
  data() {
    return {
      pokemon: null
    };
  },
  async created() {
    const pokemonId = this.$route.params.id;
    try {
      const detailsResponse = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemonId}/`);
      const details = await detailsResponse.json();
      const speciesResponse = await fetch(details.species.url);
      const speciesData = await speciesResponse.json();
      const descriptionEntry = speciesData.flavor_text_entries.find(
        entry => entry.language.name === 'es'
      );
     

      this.pokemon = {
        id: pokemonId,
        name: details.name,
        type: details.types[0].type.name,
        photo: details.sprites.front_default,
        weight: details.weight / 10, // Peso en kg
        description: descriptionEntry ? descriptionEntry.flavor_text : 'Sin descripción',
        moves: details.moves.map(move => move.move.name)
      };
    } catch (error) {
      console.error('Error encontrando Pokémon:', error);
    }
  }
};
</script>

<style scoped>
.pokemon-details {
  padding: 50px;
}
</style>
