<template>
  <div >
    <img :src="pokemonSprite" alt="" :class="{hiddenImg: !uncovered}" >
    <input v-if="!uncovered" type="text" v-model="enteredName" @keyup.enter="uncover">
    <button v-if="!uncovered" @click="uncover" >Descubrir</button>
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
      enteredName: "",
    }
  },

  /* computed:{
    //
  }, */

  methods:{
    async fetchPokemon(url){
      const { data } = await axios.get(url);
      this.pokemonName = data.name;
      this.pokemonSprite = data.sprites.front_default;
    },

    uncover(){
      console.log(this.enteredName.toLowerCase())
      console.log(this.pokemonName.toLowerCase())
      if ( this.enteredName.toLowerCase() == this.pokemonName.toLowerCase()) {
        this.uncovered = true;
      }
      else{
        alert("Nombre incorrecto")
      }
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

  
</style>