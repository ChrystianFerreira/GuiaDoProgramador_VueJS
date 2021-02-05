<template>
  <div id="app">

    <hr>
    <h3>Cadastro: </h3>
    <small v-show="deuErro" id="nomeErro">O nome é invalido!</small><br>
    <input type="text" placeholder="nome" v-model='nomeField'>  <br>
    <input type="email" placeholder="email" v-model='emailField'> <br>
    <input type="number" placeholder="idade" v-model='idadeField'> <br>
    <button @click="cadastrarUsuario">Cadastrar</button>
    <hr>

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
      deuErro: false,
      nomeField: '',
      emailField: '',
      idadeField: 0,
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
  methods: {
    cadastrarUsuario: function(){
      if(this.nomeField == "" || this.emailField == "" || this.idadeField == ""){
        this.deuErro = true;
      } else {
      this.clientes.push({
        nome: this.nomeField,
        email: this.emailField,
        idade: this.idadeField,
        id: Date.now(),
      })
      this.nomeField = ''
      this.emailField = ''
      this.idadeField = 0
      this.deuErro = false;
    }
  }
}
}
</script>

<style>
#nomeErro{
  color: red;
}
</style>