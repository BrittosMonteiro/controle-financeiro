<template>
    <div class="container">
        <div class="card">
            <input type="text" class="inputText" name="estab" id="estab" placeholder="Estabelecimento" v-model="estab">
            <input type="number" class="inputText" name="valor" id="valor" placeholder="Valor" v-model="valor">
            <button class="btnAdicionar" id="btnAdd" v-on:click="addValor">Adicionar</button>
        </div>

        <div class="group">
            <Lista v-if="entradas.length <= 0" title="Sem entradas"/>
            <Lista v-else :lista="entradas" title="Entradas"/>
            <Lista v-if="saidas.length <= 0" title="Sem saídas"/>
            <Lista v-else :lista="saidas" title="Saídas"/>
        </div>
        
        <DisplayValue title="Total" v-bind:value="total" />
    </div>
</template>

<script>
import Lista from './Lista'
import DisplayValue from './DisplayValue'

export default {
    name: 'Container',
    components:{
        Lista,
        DisplayValue,
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
            let valor = parseFloat(this.valor);

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

            this.total = (parseFloat(this.entradas.reduce((t, i) => t+i.custo, 0)))+(parseFloat(this.saidas.reduce((t, i) => t+i.custo, 0)))

            this.estab = '';
            this.valor = '';
        },
    },
    created(){
        let entradaStorage = localStorage.getItem('entradas')
        {entradaStorage != null ? this.entradas.push(...JSON.parse(entradaStorage)) : ''}

        let saidasStorage = localStorage.getItem('saidas')
        {saidasStorage != null ? this.saidas.push(...JSON.parse(saidasStorage)) : ''}

        let somaEntrada = this.entradas.reduce((soma, x) => soma+x.custo, 0);
        let somaSaida = this.saidas.reduce((soma, y) => soma + y.custo, 0);

        this.total = somaEntrada+somaSaida;
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
.group{
    display: flex;
    flex-direction: row;
    width: 100%;
    justify-content: center;
}
</style>