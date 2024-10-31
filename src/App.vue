<script>
/* import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue' */
import axios from 'axios';

export default {
  data(){
    return {
      pokemonList: [],
    }
  },

  methods:{
    async fetchPokemon(){
      const url = "https://pokeapi.co/api/v2/pokemon";
      const { data } = await axios.get(url);

      /* for(entry in data.results){
        const { subdata } = await axios.get(entry.url);
        this.pokemonList.push({
          name: subdata.results.name,
          image: subdata.results.sprites.front_default
        })
      } */

      this.pokemonList = data.results
    },
  },

  async mounted() {
    await this.fetchPokemon();
  },
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <!-- <HelloWorld msg="You did it!" /> -->
    </div>
  </header>

  <main>
    <!-- <TheWelcome /> -->
    <ul v-for="pkmn in pokemonList">
      <li>{{ pkmn.name }}</li>
    </ul>
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
