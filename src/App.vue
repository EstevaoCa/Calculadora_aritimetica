<script>
import { reactive } from 'vue';

export default {
  setup() {
    const estado = reactive({
      numero1: 0,
      numero2: 0,
      operacao: '+',
      resultado: 0,
      historico: [],
    });

    const calcular = () => {
      let resultadoCalculado;
      switch (estado.operacao) {
        case '+':
          resultadoCalculado = estado.numero1 + estado.numero2;
          break;
        case '-':
          resultadoCalculado = estado.numero1 - estado.numero2;
          break;
        case '*':
          resultadoCalculado = estado.numero1 * estado.numero2;
          break;
        case '/':
          if (estado.numero2 === 0) {
            alert("Erro: Não é possível dividir por zero!");
            return;
          }
          resultadoCalculado = estado.numero1 / estado.numero2;
          break;
      }
      estado.resultado = resultadoCalculado;
      estado.historico.push(`${estado.numero1} ${estado.operacao} ${estado.numero2} = ${estado.resultado}`);
    };

    const limparHistorico = () => {
      estado.historico = [];  // Limpa o histórico de cálculos
      estado.resultado = 0;   // Limpa o resultado
      alert("Histórico limpo!");  // Mensagem de confirmação
    };

    return { estado, calcular, limparHistorico };
  },
};
</script>

<template>
  <div id="app" class="container mt-5 p-5 border rounded">
    <h1 class="text-center">Calculadora Aritmética</h1>
    <div class="input-group mb-3">
      <input type="number" class="form-control" v-model.number="estado.numero1" placeholder="Número 1" />
      <select class="form-select" v-model="estado.operacao" @change="calcular">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>
      <input type="number" class="form-control" v-model.number="estado.numero2" placeholder="Número 2" />
    </div>
    <h2 class="text-center">Resultado: {{ estado.resultado }}</h2>
    <div class="historico mt-4">
      <h3>Histórico de Cálculos</h3>
      <ul class="list-group">
        <li v-for="(calc, index) in estado.historico" :key="index" class="list-group-item">
          {{ calc }}
        </li>
      </ul>
      <button class="btn btn-danger mt-4" @click="limparHistorico">Limpar Histórico</button>
    </div>
  </div>
</template>



<style>
* {
  text-align: center;
}
#app {
  max-width: 600px;
  margin: 0 auto;
}
</style>


