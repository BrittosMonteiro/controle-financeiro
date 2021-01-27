<template>
    <div class="container">
        <div class="card">
            <input type="text" class="inputText" name="estab" id="estab" placeholder="Estabelecimento" v-model="estab">
            <input type="number" class="inputText" name="valor" id="valor" placeholder="Valor" v-model="valor">
            <button class="btnAdicionar" id="btnAdd" v-on:click="addValor">Adicionar</button>
        </div>
        <div class="card" v-if="entradas.length <= 0">Sem entradas</div>
        <!-- <div class="card" v-else v-for="(e, index) in entradas" v-bind:key="index">{{e.estabelecimento}} - R$ {{e.custo}}</div> -->
        <Lista v-else :lista="entradas"/>
        
        <div class="card" v-if="saidas.length <= 0">Sem saídas</div>
        <!-- <div class="card" v-else v-for="(s, index) in saidas" v-bind:key="index">{{s.estabelecimento}} - R$ {{s.custo*-1}}</div> -->
        <Lista v-else :lista="saidas" />
        <div class="card" v-if="total >= 0.00">{{total}}</div>
    </div>
</template>

<script>
import Lista from './Lista'

export default {
    name: 'Container',
    components:{
        Lista
    },
    data(){
        return {
            total: 0,
            entradas: [],
            saidas:[],
            estab: '',
            valor: '',
        }
    },
    methods: {
        addValor(){
            let estab = this.estab;
            let valor = parseInt(this.valor);

            if(valor == 0  || valor == '' || valor === ''){
                return alert('Informe o valor!')
            }

            if(valor < 0){
                this.saidas.push({
                    estabelecimento: estab,
                    custo: valor
                })
                localStorage.setItem('saidas', JSON.stringify(this.saidas))
            } else {
                this.entradas.push({
                    estabelecimento: estab,
                    custo: valor
                })
                localStorage.setItem('entradas', JSON.stringify(this.entradas))
            }

            this.total = (parseInt(this.entradas.reduce((t, i) => t+i.custo, 0)))+(parseInt(this.saidas.reduce((t, i) => t+i.custo, 0)))

            this.estab = '';
            this.valor = '';
        },
    },
    created(){
        let entradaStorage = localStorage.getItem('entradas')
        if(entradaStorage != null){
            console.log(JSON.parse(entradaStorage))
            this.entradas.push(...JSON.parse(entradaStorage))
        }
    }
}
</script>

<style scoped>
.container{
    display: flex;
    flex-direction: row;
    width: 100%;
    align-items: flex-start;
    justify-content: space-between;
}
.card{
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 200px;
    padding: 10px;
    align-items: center;
    justify-content: flex-start;
    border: 1px solid #ccc;
}
.inputText{
    padding: 5px 10px;
    border-radius: 3px;
    margin-bottom: 5px;
    border: 1px solid #ccc;
}
.card button{
    padding: 5px;
    background-color: #1111ff;
    border-radius: 3px;
    color: #eee;
}
</style>