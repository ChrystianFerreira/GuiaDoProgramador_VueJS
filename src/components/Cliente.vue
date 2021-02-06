<template>
    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <h4>Nome: {{cliente.nome}}</h4>
        <p>Email: {{cliente.email | processarEmail}}</p>
        <p v-if="showIdade == true">Idade: {{cliente.idade}}</p>
        <p v-else>Esse usuário escondeu a idade</p>
        <button @click="mudarCor($event)">Mudar cor</button>
        <button @click="emitirEventoDelete">Deletar</button>
        <h4>Id especial gerado pelas computed properties: {{idEspecial}}</h4>
    </div>
</template>

<script>
export default {
    data(){
        return{
            isPremium: false
        }
    },
    props: {
        cliente: Object,
        showIdade: Boolean
    },
    methods: {
        mudarCor: function($event){
            console.log($event)
            this.isPremium = !this.isPremium;
        },
        emitirEventoDelete: function(){
            console.log("!  - - - - Emitindo evento no filho - - - -  !");
            this.$emit("meDelete", {idDoCliente: this.cliente.id, component: this})
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
        processarEmail(value){
            return value.toUpperCase();
        }
    },
    computed: {
        idEspecial: function(){
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
}
</script>
<style scoped>
    .cliente{
        background-color:#ECE5E3;
        color:black;
        max-width:600px;
        height: 200px;
        padding: 1%;
        margin-top: 2%; 
    }

    .cliente-premium{
        background-color:#3d3d3d;
        color:yellow;
        max-width:600px;
        height: 200px;
        padding: 1%;
        margin-top: 2%; 
    }
</style>