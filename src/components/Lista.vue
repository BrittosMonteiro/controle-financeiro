<template>
    <div class="lista">
        <h1 class="listTitle">{{title}}</h1>
        <ol class="list">
            <li class="listItem" v-for="(l, index) in lista" v-bind:key="index">{{l.estabelecimento}} - R$ {{l.custo}}</li>
        </ol>
    </div>
</template>

<script>
export default {
    name: 'Lista',
    props:{
        title: String,
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
    background-color: #123;
    box-shadow: 0 0 0.3em #444;
    margin: 0 5px;
    padding: 10px;
}
.listTitle{
    display: flex;
    justify-content: center;
    font-size: 24px;
    color: #f6f4eb;
}
.listItem{
    display: flex;
    padding: 5px;
    margin: 5px 0;
    color: #f6f4eb;
    background-color: #345;
    border-radius: 3px;
}
</style>