<template>
  <div id="app">
    <div v-for="(pokemon, index) in pokemons" :key="index">
      <h4>{{index+1}} {{pokemon.name}}</h4>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return{
      pokemons: []
    }
  },
  created: function () {
    console.log("Rodando axios.get - Dentro de created: function()")
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results
    });
  },
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
}
</style>
