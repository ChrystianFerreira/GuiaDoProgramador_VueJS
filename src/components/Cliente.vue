<template>
    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <h4>Nome: {{cliente.nome}}</h4>
        <p>Email: {{cliente.email}}</p>
        <p v-if="showIdade == true">Idade: {{cliente.idade}}</p>
        <p v-else>Esse usuário escondeu a idade</p>
        <button @click="mudarCor($event)">Mudar cor</button>
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
        }
    }
}
</script>
<style scoped>
    .cliente{
        background-color:#ECE5E3;
        color:black;
        max-width:600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%; 
    }

    .cliente-premium{
        background-color:#3d3d3d;
        color:yellow;
        max-width:600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%; 
    }
</style>