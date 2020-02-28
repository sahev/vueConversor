<template>
  <div>
    <div class="container-title">
      <select id="moedas" v-model="moedaAType">
        <option v-for="moeda in moedas" :key="moeda.id" :value="moeda.name">{{ moeda.name }}</option>
      </select>
      <h2>Para</h2>
      <select id="moedas" v-model="moedaBType">
        <option
          v-show="moeda.name !== moedaAType"
          v-for="moeda in moedas"
          :key="moeda.id"
          :value="moeda.name"
        >{{ moeda.name }}</option>
      </select>
    </div>
    <input type="text" v-model="moedaValue" :placeholder="moedaAType" @keydown="converter" />
    <!-- <input type="button" value="Converter" @click="converter" /> -->
    <h2>R$ {{result}}</h2>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Conversor",
  data() {
    return {
      moedaAType: "",
      moedaBType: "",
      moedas: [
        { id: 1, name: "BRL" },
        { id: 2, name: "USD" },
        { id: 3, name: "NZD" }
      ],
      moedaValue: "",
      result: 0
    };
  },
  methods: {
    converter() {
      if (this.moedaValue === "") {
        alert("Coloque o valor desejado");
      }
      if (this.moedaAType === this.moedaBType) {
        alert("Moedas iguais");
      }
      
      let url = `https://api.exchangeratesapi.io/latest?base=${this.moedaAType}`;

      // fetch(url)
      //   .then(res => {
      //     return res.json();
      //   })
      //   .then(json => {
      //     let cotacaoA = json.rates[this.moedaBType];
      //     this.result = (cotacaoA * this.moedaValue).toFixed(2);
      //   });

      axios.get(url).then(res => {
          console.log(res);
          
          let cotacaoA = res.data.rates[this.moedaBType];
          this.result = (cotacaoA * this.moedaValue).toFixed(2);
        });
    }
  }
};
</script>

<style scoped>
.container-title {
  display: flex;
  justify-content: center;
  padding-bottom: 1rem;
}
</style>