<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/Pokemon-Logo.png" alt="">
      <input class="input is-rounded" v-model="busca" type="text" placeholder="Buscar pokemon pelo nome">
      <button class="button is-fullwidth is-success" id="buscaBtn">Buscar</button>
      <div v-for="(pokemon,index) in resultadoBusca" v-bind:key="index">
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
      pokemons: [],
      busca: ''
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
    
  },
  computed: {
    resultadoBusca() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
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

#buscaBtn {
  margin-top: 2%;
}
</style>
