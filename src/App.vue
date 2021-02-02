<template>
  <div id="app">
    <h1>Guia clientes</h1>
    <div v-for="(cliente, index) in clientes" :key="cliente.id">
      <h2>{{index + 1}}</h2>
      <Cliente :showIdade='true' :cliente="cliente"/>
      <h4>Edição: </h4>
      <input type="text" v-model="cliente.nome">
      <input type="text" v-model="cliente.email">
    </div>
    <h1>Lista de produtos</h1>
    <Produto></Produto>
  </div>
</template>

<script>
import Cliente from "./components/Cliente.vue";
import Produto from "./components/Produto.vue";

export default {
  name: "App",
  data() {
    return {
      nomeDoVictor: "Victor O. Lima",
      clienteChrys: {
        nome: "Chrystian Ferreira",
        email: "chrystian.profissional@gmail.com",
        idade: 19,
      },
      clientes: [
        {
          id: 1,
          nome: "Chrystian Vacancy",
          email: "chrystian.a@gmail.com",
          idade: 19,
        },
        {
          id: 2,
          nome: "Chrystian Finances",
          email: "chrystian.b@gmail.com",
          idade: 20,
        },
        {
          id: 3,
          nome: "Chrystian Buildings",
          email: "chrystian.c@gmail.com",
          idade: 21,
        },
      ],
    };
  },
  components: {
    Cliente,
    Produto,
  },
};
</script>

<style>
#app {
}
</style>



aaaaaawwwwwwwwwwwwwwwwwweeeeeqqqqqqqqeeeeeeeeeeeeeettttttt