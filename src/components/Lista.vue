<template>
    <div class="lista">
        <p v-for="(l, index) in lista" v-bind:key="index">{{l.estabelecimento}} - {{l.custo}}</p>
    </div>
</template>

<script>
export default {
    name: 'Lista',
    props:{
        lista: Array
    }
}
</script>

<style scoped>
.lista{
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 200px;
    background-color: #345;
    padding: 10px;
}
</style>