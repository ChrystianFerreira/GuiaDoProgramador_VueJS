<template>
    <div id="cliente">
        <input type="text" :value="nome">
        <hr>
        <input type="text" :value="descricao">
        <h2>{{nome}}</h2>
        <h3>{{descricao}}</h3>
        {{2 + 2 * 2}}
    </div>
</template>

<script>
export default {
    data(){
        return{
            nome: "Chrystian",
            numero: "",
            email: "",
            idade: 0,
            descricao: "Lorem ipsum"
        }
    }
}
</script>

<style scoped>
    #cliente{
        color:black;
        background-color: gray;
    }
</style>