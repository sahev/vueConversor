 

<template>
  <div class="conversor">
    <h2>
      <select v-model="moedaAtype">
        <option v-for="moeda in moedas" :key="moeda.id">{{moeda.name}}</option>
      </select>
    </h2>

    <h2>Para</h2>

    <h2>
     <select v-model="moedaBtype">
  
        <option v-show="moeda.name !== moedaAtype" v-for="moeda in moedas" :key="moeda.id">{{moeda.name}}</option>
      </select>
    </h2>

    <input type="text" v-model="moedaA_value" @keypress.enter="converter"/>

    <input type="button" value="Converter" v-on:click="converter" />

    <div v-if="moedaBtype === 'USD'">
      <h2>US${{valor}}</h2>
    </div>
    <div v-if="moedaBtype === 'NZD'">
      <h2>NZ${{valor}}</h2>
    </div>
    <div v-if="moedaBtype === 'BRL'">
      <h2>R${{valor}}</h2>
    </div>  
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Conversor",
  data() {
    return {
      moedaAtype: "",
      moedaBtype: "",
      moedaA_value: 0,
      valor: 0,
      moedas: [
                {id: 1, name: "USD"}, 
                {id: 2, name: "BRL" }, 
                {id: 3, name: "NZD"}
              ],
      results: []
    };
  },

  methods: {
    converter() {
      let url = `https://api.exchangeratesapi.io/latest?base=${this.moedaAtype}`;

      axios.get(url).then(res => {
        this.results = res.data.rates;
        let conversao = this.moedaA_value * res.data.rates[this.moedaBtype];
        this.valor = conversao.toFixed(2)
      });
    }
  }
};
</script>

<style scoped>
</style>