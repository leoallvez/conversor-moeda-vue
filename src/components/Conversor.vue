<template>
    <div class="conversor">
        <h2>{{ moedaA }} para {{ moedaB }}</h2>
        <input type="number" v-model="valorParaConversao" :placeholder="`Converter ${moedaA}`">
        <input type="button" value="Converter" v-on:click="converter">
        <h2> {{ resultado == 0 ? '0.00' : resultado }} </h2>
    </div>
</template>

<script>
export default {
    name: "Conversor",
    props: ["moedaA", "moedaB"],
    data() {
        return {
            valorParaConversao: "",
            resultado: 0
        }
    },
    methods: {
        converter() {

            let dePara = `${this.moedaA}_${this.moedaB}`
            let url = `https://free.currconv.com/api/v7/convert?q=${dePara}&compact=ultra&apiKey=9d8897b0c45aa426cac7`

            fetch(url).then(res => res.json()).then(json => {
                if(this.valorParaConversao != "") { 
                    let cotacao = json[dePara]
                    this.resultado = (cotacao * parseFloat(this.valorParaConversao)).toFixed(2).toString()
                }else{
                    this.resultado = 0;
                }
            })
    
        }
    }
}
</script>

<style scoped>
    .conversor {
        padding: 20px;
        max-width: 300px;
        box-shadow: 0 4px 8px 0 rgb(0, 0, 0, 0.2)
    }

</style>