<script>
import Pokemon from './components/Pokemon.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Pokemon
  },

  data(){
    return {
      pokemonList: [],
    }
  },

  methods:{
    async fetchPokemonList(){
      //console.log(this.pokemonList)
      const url = "https://pokeapi.co/api/v2/pokemon";
      const { data } = await axios.get(url);
      this.pokemonList = data.results;
      //console.log(this.pokemonList);
    },
  },

  async mounted() {
    await this.fetchPokemonList();
  },
}
</script>

<template>
  <header>
    <h1>¿Quién es ese Pokémon?</h1>
    <h4>Pokémones descubiertos: <span>0</span></h4>
  </header>

  <main v-for="(pkmn, index) in pokemonList">
    <Pokemon :pokemon="pkmn" />
  </main>
</template>

<style scoped>
  /*
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
*/
</style>
