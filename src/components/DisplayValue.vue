<template>
    <div class="displayValue">
        <h1 class="displayValueTitle">{{title}}</h1>
        <span v-if="value > 0.00" class="displayValueShown green">R$ {{parseFloat(value.toFixed(2))}}</span>
        <span v-else-if="value < 0.00" class="displayValueShown red">R$ {{parseFloat(value.toFixed(2))}}</span>
        <span v-else class="displayValueShown white">Sem variação</span>
    </div>
</template>

<script>
export default {
    name: 'DisplayValue',
    props:{
        title: String,
        value: Number,
    },
}
</script>

<style scoped>
.displayValue{
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 200px;
    background-color: #123;
    padding: 10px;
    border-radius: 3px;
    box-shadow: 0 0 0.3em #345;
}
.displayValueTitle{
    display: flex;
    justify-content: center;
    color: #f6f4eb;
    font-size: 24px;
}
.displayValueShown{
    display: flex;
    justify-content: center;
    margin: 10px 0;
    font-weight: bold;
    font-size: 18px;
}
</style>