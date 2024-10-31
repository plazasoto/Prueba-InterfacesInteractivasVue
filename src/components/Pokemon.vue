<template>
  <div>
    <img :src="pokemonSprite" alt="">
    {{ pokemonName }}
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props:{
    pokemon: {},
  },
  data(){
    return {
      pokemonName: "",
      pokemonSprite: "",
    }
  },

  methods:{
    async fetchPokemon(url){
      const { data } = await axios.get(url);
      this.pokemonName = data.name;
      this.pokemonSprite = data.sprites.front_default;
    },
  },

  async mounted() {
    await this.fetchPokemon(this.pokemon.url);
  },
}
</script>