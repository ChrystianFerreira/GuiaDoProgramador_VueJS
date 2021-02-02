<template>
    <div id="cliente">
        <h4>Nome: {{cliente.nome}}</h4>
        <p>Email: {{cliente.email}}</p>
        <p v-show="showIdade == true">Idade: {{cliente.idade}}</p>
        <!-- <p v-else>Esse usuário escondeu a idade</p> 
              /\ Deve estar logo abaixo de um v-if

            <p v-else-if="...">...</p>        
            /\ Podem existir quantos quiser, desde que abaixo de um if
         -->

    </div>
</template>

<script>
export default {
    data(){
        return{
            
        }
    },
    props: {
        cliente: Object,
        showIdade: Boolean
    }
}
</script>
<style scoped>
    #cliente{
        background-color:#ECE5E3;
        color:black;
        max-width:600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%; 
    }
</style>