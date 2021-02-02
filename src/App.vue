<template>
  <div id="app">
    <h1>Guia clientes</h1>
    <Cliente :cliente="clienteChrys"
    ></Cliente>
    <h1>Lista de produtos</h1>
    <Produto></Produto>
  </div>
</template>

<script>
import Cliente from './components/Cliente.vue'
import Produto from './components/Produto.vue'


export default {
  name: 'App',
  data(){
    return {
      nomeDoVictor: "Victor O. Lima",
      clienteChrys: {
        nome: "Chrystian Ferreira",
        email: "chrystian.profissional@gmail.com",
        idade: 19
      }
    }
  },
  components: {
    Cliente,
    Produto
  }
}
</script>

<style>
#app {
  
}
</style>