<template>
    <div class="displayValue">
        <h1 class="displayValueTitle">{{title}}</h1>
        <span v-if="value > 0.00" class="">R$ {{value}}</span>
        <span v-else-if="value < 0.00" class="">R$ {{value}}</span>
        <span v-else class="">Nada</span>
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
    background-color: #234;
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
</style>