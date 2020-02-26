<template>

    <div class="conversor">

        <h2>{{moedaA}} Para {{moedaB}}</h2>
        <input type ="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
        <input type="button" value="Converter" v-on:click="converter">
        <h2>R$ {{moedaB_value}}</h2>
    </div>
</template>

<script>
export default {
     name: "Conversor",
     props: ["moedaA","moedaB"],
        data(){
            return{
                moedaA_value: "",
                moedaB_value: 0
            
            };
            
        },
        
methods: {
    converter(){
        console.log("converter method "+this.moedaB_value+"");
        let a = this.moedaA;
        let b = this.moedaB;
        let url = "https://api.exchangeratesapi.io/latest?symbols="+a+","+b+"";

        fetch(url)
            .then(res => {
                return res.json();
        })
        .then(json => {
            console.log(json);
            let cotacao = json["rates"].BRL;
            
            let cotacaobrl = json["rates"].BRL;
            let cotacaousd = json["rates"].USD;

            //this.moedaB_value = (cotacao * this.moedaA_value);
            this.moedaB_value = (cotacao * this.moedaA_value).toFixed(2);

            console.log("cotacao BRL "+cotacaobrl+"; cotacao USD "+cotacaousd+"");
            console.log("converter method "+this.moedaA_value+" "+this.moedaB_value+"");

        });
    }
}
};


</script>

<style scoped>

</style>