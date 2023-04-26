<template>
  <div class="container grid-lg my-2 py2 text-dark">
    <div class="card">
      <div class="card-header">
        <h1> Cotações das Moedas </h1>
      </div>
      <div class="card-body">
        <CotacoesMoedas :quotes="quotes" />
      </div>
    </div>
  </div>
</template>

<script>

import CotacoesMoedas from './components/CotacoesMoedas.vue';
import api from '@/servidor/api.js';
import { onMounted, reactive, toRefs } from 'vue';


export default {
  name: 'App',

  components: {
    CotacoesMoedas
  },

  // expor os dados da API no componente
  setup() {

    const data = reactive ({  // dados reativos
        quotes: { },   //quotes são referentes as moedas
    });

    onMounted( async() => {  //após o componente ser montado
        const response = await api.all();
        data.quotes = response.data;
    })

    return { ...toRefs(data) } //vai retornar os dados(data)

  }

}
</script>

<style>
  .card {
    box-shadow:  inset 0 0 1em black;
  }
  .card-header{
    font-size: 30px;
    padding: 30px;
    text-align: center;
    margin-bottom: 10px;
    position: relative;
    top: 20px;
  }
</style>
