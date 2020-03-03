 

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

    <input type="text" v-model="moedaA_value" />

    <input type="button" value="Converter" v-on:click="converter" />

    <h2>$ {{valor}}</h2>
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
      moedas: ["USD", "BRL", "NZD"],
      results: [],
      mueda: {}
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