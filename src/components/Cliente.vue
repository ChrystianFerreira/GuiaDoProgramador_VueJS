<template>
  <div :class="{ cliente: !isPremium, 'cliente-premium': isPremium }">
    <h4>Nome: {{ cliente.nome }}</h4>
    <p>Email: {{ cliente.email | processarEmail }}</p>
    <p v-if="showIdade == true">Idade: {{ cliente.idade }}</p>
    <p v-else>Esse usuário escondeu a idade</p>
    <h4>Id especial gerado pelas computed properties: {{ idEspecial }}</h4>
    <button
      @click="emitirEventoDelete"
      style="margin-right: 5px"
      class="button is-danger is-small"
    >
      Deletar
    </button>
    <button
      @click="mudarCor($event)"
      class="button is-warning is-light is-small"
    >
      Tornar premium (mudar cor)
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isPremium: false,
    };
  },
  props: {
    cliente: Object,
    showIdade: Boolean,
  },
  methods: {
    mudarCor: function ($event) {
      console.log($event);
      this.isPremium = !this.isPremium;
    },
    emitirEventoDelete: function () {
      console.log("!  - - - - Emitindo evento no filho - - - -  !");
      this.$emit("meDelete", { idDoCliente: this.cliente.id, component: this });
    },
  },
  /*
    Essa maneira de usar filtros está depreciada, de acordo com a documentação
    do Vue 3.x em diante presente em v3.vuejs.org: 'In 3.x, filters are removed
    and no longer supported. Instead, we recommend replacing them with method calls
    or computed properties.'

    Esse 'filtro' na verdade é mais como um pós-processamento dos dados recebidos
    antes da exibição deles na tela.
    */
  filters: {
    processarEmail(value) {
      return value.toUpperCase();
    },
  },
  computed: {
    idEspecial: function () {
      return (
        this.cliente.email +
        this.cliente.nome +
        this.cliente.id
      ).toUpperCase();
    },
  },
};
</script>
<style scoped>
.cliente {
  margin: 10px 0 10px 5px;
  border: 1px solid rgb(0, 0, 255);
  border-radius: 4px;
  padding: 15px 10px 5px 10px;
  background-color: #00ffff;
  color: black;
  width: 600px;
  height: 175px;
  padding: 1%;
}

.cliente-premium {
  margin: 10px 0 10px 5px;
  border: 1px solid rgb(224, 177, 255);
  border-radius: 4px;
  padding: 15px 10px 5px 10px;
  background-color: #f7ff8e;
  color: black;
  width: 600px;
  height: 175px;
  padding: 1%;
}
</style>