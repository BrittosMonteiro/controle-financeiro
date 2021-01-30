<template>
    <div class="container">
        <div class="card">
            <button class="btnNewInformation" @click="btnNewInformation">
                + Nova informação
            </button>
            <div class="formNewInformation" v-if="visible">
                <input type="text" class="inputText" name="origin" id="origin" placeholder="Origem" v-model="origin" autofocus>
                <input type="number" class="inputText" name="valor" id="valor" placeholder="Valor" v-model="valor">
                <select name="category" class="inputText" v-model="categoria">
                    <option value="">Categoria</option>
                    <option value="entrada">Entrada</option>
                    <option value="saida">Saída</option>
                </select> 
                <button class="btnAdd" id="btnAdd" v-on:click="addValor">Adicionar</button>
            </div>
        </div>
        
        <DisplayValue title="Total" v-bind:value="total" />

        <div class="group">
            <Lista v-if="entradas.length <= 0" title="Sem entradas"/>
            <Lista v-else :lista="entradas" title="Entradas"/>
            <Lista v-if="saidas.length <= 0" title="Sem saídas"/>
            <Lista v-else :lista="saidas" title="Saídas"/>
        </div>

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
            origin: '',
            valor: '',
            categoria: '',
            visible: false
        }
    },
    methods: {
        btnNewInformation(){
            this.visible = !this.visible;
        },
        addValor(){
            let origin = this.origin;
            let valor = parseFloat(this.valor);
            let categoria = this.categoria;

            if(valor == 0  || valor == '' || valor === ''){
                return alert('Informe o valor!')
            }

            if(categoria == '' || categoria === ''){
                return alert('Informe a categoria')
            }

            if(valor < 0){
                this.saidas.push({
                    origin: origin,
                    custo: valor
                })
                localStorage.setItem('saidas', JSON.stringify(this.saidas))
            } else {
                this.entradas.push({
                    origin: origin,
                    custo: valor
                })
                localStorage.setItem('entradas', JSON.stringify(this.entradas))
            }

            this.total = (parseFloat(this.entradas.reduce((t, i) => t+i.custo, 0)))+(parseFloat(this.saidas.reduce((t, i) => t+i.custo, 0)))

            this.origin = '';
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
    flex-direction: column;
    width: 100%;
    align-items: flex-start;
    justify-content: space-between;
    margin:15px 0;
}
.card{
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    width: 100%;
    justify-content: flex-start;
    margin: 0 0 15px 0;
}
.formNewInformation{
    display: flex;
    margin: 10px 0;
    flex-wrap: wrap;
}
.inputText{
    padding: 5px 10px;
    width: 200px;
    height: 35px;
    margin: 0 15px 0 0;
    border-radius: 1px;
    background-color: #101010;
    border: 1px solid transparent;
    color: #f6f4eb;
    transition: all 0.6s ease-in-out;
}
.inputText::placeholder{
    color: #f6f4eb;
    font-style: italic;
}
.inputText:focus{
    border: 1px solid #f33
}
.btnAdd, .btnNewInformation{
    height: 35px;
    padding: 5px;
    background-color: #f33;
    color: #eee;
    border-radius: 2px;
}
.btnNewInformation{
    width: 150px;
    font-weight: 600;
}
.group{
    display: flex;
    flex-direction: row;
    width: 100%;
    justify-content: space-between;
}
</style>