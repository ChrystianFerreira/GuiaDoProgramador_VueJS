<template>
  <div id="app">
    <div id="input">
      <h1 style="fontSize: 35px">Vue Pokédex</h1>
      <input
        id="pokemonSearchInput"
        class="input is-rounded"
        type="text"
        placeholder="Busque um Pokemon"
        v-model="busca"
      />
      <button
        style="background: rgb(251,255,152); background: radial-gradient(circle, rgba(251,255,152,1) 68%, rgba(252,255,122,1) 95%, rgba(253,228,84,1) 100%); borderColor: #fde454;"
        class="button is-rounded is-small is-fullwidth mt-2 mb-2"
        @click="buscar"
      >
        Buscar
      </button>
    </div>
    <div id="list">
      <div id="pokemon" v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
        <Pokemon :type="pokemon.type" :name="pokemon.name" :url="pokemon.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function () {
    console.log("Rodando axios.get - Dentro de created: function()");
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function () {
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca.toLowerCase()
        );
      }
    },
  },
  computed: {
    //  resultadoBusca: function(){
    //    if(this.busca == '' || this.busca == ' '){
    //      return this.pokemons;
    //    } else {
    //      return this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
    //    }
    //  }
  },
};
</script>

<style>
#input {
  width: 500px;
  margin: auto;
}
#pokemon {
  margin: 5px;
}
#list {
  margin: 0 3% 0 3%;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
  -webkit-flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  -webkit-justify-content: space-between;
  -ms-flex-pack: distribute;
  justify-content: space-between;
  -webkit-align-content: flex-start;
  -ms-flex-line-pack: start;
  align-content: flex-start;
  -webkit-align-items: flex-start;
  -ms-flex-align: start;
  align-items: flex-start;
}

#app {
  background: #e5ffff;
  background: linear-gradient(180deg, rgba(229,255,255,1) 0%, rgba(236,254,255,1) 35%, rgba(144,236,255,1) 100%);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  image-rendering: -moz-crisp-edges;
  image-rendering: -webkit-crisp-edges;
  image-rendering: pixelated;
  image-rendering: crisp-edges;
}
</style>
