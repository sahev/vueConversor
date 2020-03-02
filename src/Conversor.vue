<template>

    <div class="conversor">

        <h2>
            <select v-model="moedaAtype">
                <option v-for="moeda in moedas" :key="moeda">{{moeda}}</option>
            </select>
        </h2>
        
        <h2>Para</h2>
        
        <h2>
            <select v-model="moedaBtype">
                <option v-for="moeda in moedas" :key="moeda">{{moeda}}</option>
            </select>
        </h2>

        <input type="text" v-model="moedaA_value">

        <input type="button" value="Converter" v-on:click="converter">
        
        <h2>R$ {{valor}}</h2>

        
    </div>
</template>

<script>

export default {
     name: "Conversor",
        data(){
            return{
                moedaAtype: "",
                moedaBtype: "",
                moedaA_value: 0,
                valor: 0,
                moedas: ['USD', 'BRL', 'NZD']
            };

            
        },
        
methods: {
    
    converter(){

        let a = this.moedaAtype;
        let b = this.moedaBtype;
        let url = "https://api.exchangeratesapi.io/latest?base="+a+"";

       
        fetch(url)
            .then(res => {
                return res.json();
        })
        .then(json => {

            let cotacao = json["rates"].b;

            //this.moedaB_value = (cotacao * this.moedaA_value);
            this.valor = (cotacao * this.moedaA_value).toFixed(2);

            console.log(json);
          
           console.log(a,b,this.moedaA_value,cotacao);

        });
    },
    


}

};


</script>

<style scoped>

</style>