<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(pokemon,index) in pokemons" v-bind:key="index">
        <Pokemon v-bind:name="pokemon.name" v-bind:url="pokemon.url" v-bind:num="index + 1"/>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data(){
    return {
      pokemons: []
    }
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista de pokemons")
      this.pokemons = res.data.results
    })
  },
  components: {
    Pokemon
    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
