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
      counter: 0,
    }
  },

  computed:{
    pokeCounter(){
      return this.counter;
    }
  },

  methods:{
    async fetchPokemonList(){
      //consigue lista de 20
      const url = "https://pokeapi.co/api/v2/pokemon";
      const { data } = await axios.get(url);
      this.pokemonList = data.results;
    },

    countUp(){
      this.counter++;
    }
  },

  async mounted() {
    await this.fetchPokemonList();
  },
}
</script>

<template>
  <header>
    <h1>¿Quién es ese Pokémon?</h1>
    <h4>Pokémones descubiertos: <span class="counter">{{ pokeCounter }}</span></h4>
  </header>

  <main v-for="(pkmn, index) in pokemonList">
    <Pokemon :pokemon="pkmn" @count-up="countUp"/>
  </main>
</template>

<style scoped>
  .counter{
    color: blue;
  }
</style>
