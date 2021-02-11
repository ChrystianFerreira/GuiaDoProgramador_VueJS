<template>
  <div class='column is-half is-offset-one-quarter' id="app">
    <h1>Pokedex</h1>
    <input id="pokemonSearchInput" class="input is-rounded" type="text" placeholder="Busque um Pokemon" v-model="busca">
    <button class="button is-rounded is-small is-fullwidth mt-1" @click=buscar >Buscar</button>
    <div >
      <div v-for="(pokemon, index) in filteredPokemons" :key="index">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index + 1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from './components/Pokemon'

export default {
  name: "App",
  data() {
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function () {
    console.log("Rodando axios.get - Dentro de created: function()")
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    });
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function() {
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      } else {
         this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
      }
    }
  },
  computed: {
  //  resultadoBusca: function(){
  //    if(this.busca == '' || this.busca == ' '){
  //      return this.pokemons;
  //    } else {
  //      return this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
  //    }
  //  }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  image-rendering: -moz-crisp-edges;
  image-rendering: -webkit-crisp-edges;
  image-rendering: pixelated;
  image-rendering: crisp-edges;
}
</style>
