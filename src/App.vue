<template>
  <div id="app">
    <!-- Cadastro de usuários -->
    <hr />
    <h3>Cadastro:</h3>
    <small v-show="deuErro" id="nomeErro">O nome é invalido!</small><br />
    <input type="text" placeholder="nome" v-model="nomeField" /> <br />
    <input type="email" placeholder="email" v-model="emailField" /> <br />
    <input type="number" placeholder="idade" v-model="idadeField" /> <br />
    <button @click="cadastrarUsuario">Cadastrar</button>
    <hr />
    <!-- Fim do cadastro -->

    <!-- Visualização de usuários -->
    <h1>Guia clientes</h1>
    <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
      <h2>{{ index + 1 }}</h2>
      <Cliente
        :showIdade="true"
        :cliente="cliente"
        @meDelete="deletarUsuario($event)"
      />
    </div>
    <!-- Fim da visualização -->
  </div>
</template>

<script>
import Cliente from "./components/Cliente.vue";
import _ from "lodash";

export default {
  name: "App",
  data() {
    return {
      deuErro: false,
      nomeField: "",
      emailField: "",
      idadeField: 0,
      clientes: [
        {
          id: 1,
          nome: "Ahrystian Vacancy",
          email: "chrystian.a@gmail.com",
          idade: 19,
        },
        {
          id: 2,
          nome: "Bhrystian Finances",
          email: "chrystian.b@gmail.com",
          idade: 20,
        },
        {
          id: 3,
          nome: "Chrystian Buildings",
          email: "chrystian.c@gmail.com",
          idade: 21,
        },
        {
          id: 4,
          nome: "Arrzo Vacancy",
          email: "chrystian.a@gmail.com",
          idade: 22,
        },
        {
          id: 5,
          nome: "Btata Finances",
          email: "chrystian.b@gmail.com",
          idade: 23,
        },
        {
          id: 6,
          nome: "Feijão Buildings",
          email: "chrystian.c@gmail.com",
          idade: 24,
        },
      ],
    };
  },
  components: {
    Cliente,
  },
  methods: {
    cadastrarUsuario: function () {
      if (
        this.nomeField == "" ||
        this.emailField == "" ||
        this.idadeField == ""
      ) {
        this.deuErro = true;
      } else {
        this.clientes.push({
          nome: this.nomeField,
          email: this.emailField,
          idade: this.idadeField,
          id: Date.now(),
        });
        this.nomeField = "";
        this.emailField = "";
        this.idadeField = 0;
        this.deuErro = false;
      }
    },
    deletarUsuario: function ($event) {
      console.log("! - Evento emitido no filho chegou ao pai. - !");
      this.clientes = this.clientes.filter(
        (cliente) => cliente.id != $event.idDoCliente
      );
    },
  },
  computed: {
    orderClientes: function() {
      return _.orderBy(this.clientes,[item => item.nome.toLowerCase()],['asc']);
    }
  }
};
</script>

<style>
#nomeErro {
  color: red;
}
</style>