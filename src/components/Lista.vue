<template>
    <div class="lista">
        <div class="listHeading">
            <h1 class="listTitle">{{title}}</h1>
            <span v-if="title == 'Entradas'" class="listTotal green">R$ {{total}}</span>
            <span v-if="title == 'Saídas'" class="listTotal red">R$ {{total}}</span>
        </div>
        <ol class="list">
            <li class="listItem" v-for="(l, index) in lista" v-bind:key="index">
                {{l.origin}} - R$ {{l.custo}}
            </li>
        </ol>
    </div>
</template>

<script>
export default {
    name: 'Lista',
    props:{
        title: String,
        lista: Array
    },
    data(){
        return{
            total: this.lista.reduce((x, i) => x+i.custo, 0)
        }
    }
}
</script>

<style scoped>
.lista{
    display: flex;
    flex-direction: column;
    width: 49%;
    background-color: #171717;
    box-shadow: 0 0 0.2em #333;
    margin: 15px 0 0 0;
    padding: 10px;
    border-radius: 3px;
}
.listHeading{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
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
    margin: 10px 0;
    color: #f6f4eb;
    background-color: #111;
    border-radius: 3px;
}
</style>