<template>
  <div >
    <img :src="pokemonSprite" alt="" :class="{hiddenImg: !uncovered}" >
    <input v-if="!uncovered" type="text" name="" id="" >
    <button v-if="!uncovered" >Descubrir</button>
    <p v-if="uncovered"> {{ pokemonName }} </p>
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
      uncovered: false,
    }
  },

  methods:{
    async fetchPokemon(url){
      const { data } = await axios.get(url);
      this.pokemonName = data.name;
      this.pokemonSprite = data.sprites.front_default;
    },

    uncover(){
      //
    },
  },

  async mounted() {
    await this.fetchPokemon(this.pokemon.url);
  },
}
</script>

<style scoped>
  .hiddenImg{
    filter: blur(5px) grayscale(100%);
  }

/*   .block{
    display: block;
  } */
</style>