<template>
    <div>
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