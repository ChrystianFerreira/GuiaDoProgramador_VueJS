<template>
  <div id="app">
    <!-- Cadastro de usuários -->
    <div :class="{ form: !deuErro, formDeuErro: deuErro }">
      <h3 style="margin-left: 0.25rem">Cadastro</h3>
      <small
        style="margin-left: 0.25rem; color: red"
        v-show="deuErro"
        id="nomeErro"
      >Dados invalidos!
      </small><br/>
      <p>Nome</p>
      <input
        type="text"
        placeholder="Insira seu nome"
        v-model="nomeField"
        :class="{
          'input is-primary mx-1 my-1': !deuErro,
          'input is-danger mx-1 my-1': deuErro,
        }"
      />
      <br />
      <p>E-Mail</p>
      <input
        type="email"
        placeholder="Insira seu e-mail"
        v-model="emailField"
        :class="{
          'input is-primary mx-1 my-1': !deuErro,
          'input is-danger mx-1 my-1': deuErro,
        }"
      />
      <p>Idade</p>
      <input
        type="number"
        v-model="idadeField"
        :class="{
          'input is-przimary mx-1 my-1': !deuErro,
          'input is-danger mx-1 my-1': deuErro,
        }"
      />
      <button
        class="button is-primary is-small"
        style="margin-left: 0.25rem"
        @click="cadastrarUsuario"
      >
        Cadastrar
      </button>
    </div>
    <!-- Fim do cadastro -->

    <!-- Visualização de usuários -->
    <h1>Guia clientes</h1>
    <div v-for="cliente in orderClientes" :key="cliente.id">
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
    orderClientes: function () {
      return _.orderBy(this.clientes,[(item) => item.nome.toLowerCase()],["asc"]);
    },
  },
};
</script>

<style>
.form {
  margin: 5px;
  border: 1px solid rgb(0, 0, 255);
  border-radius: 4px;

  padding: 15px 10px 5px 10px;
  background-color: #dce2ff;
  width: 400px;
  height: 320px;
}

.formDeuErro {
  margin: 5px;
  border: 1px solid red;
  border-radius: 4px;

  padding: 15px 10px 5px 10px;
  background-color: #ffb56f;
  width: 400px;
  height: 320px;
}
</style>