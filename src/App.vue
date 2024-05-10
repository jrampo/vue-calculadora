<script setup>
import { reactive, watch } from "vue";

const estado = reactive({
  num1: 0,
  num2: 0,
  operacao: "somar",
  resultado: null,
});

const realizaOperacao = () => {
  const { num1, num2, operacao } = estado;

  switch (operacao) {
    case "somar":
      estado.resultado = parseInt(num1) + parseInt(num2);
      break;
    case "subtrair":
      estado.resultado = parseInt(num1) - parseInt(num2);
      break;
    case "multiplicar":
      estado.resultado = parseInt(num1) * parseInt(num2);
      break;
    case "dividir":
      estado.resultado = parseInt(num1) / parseInt(num2);
      break;
    default:
      estado.resultado = null;
      console.log("Operação inválida");
  }
};

watch(
  () => [estado.num1, estado.num2, estado.operacao],
  () => {
    realizaOperacao();
  }
);
</script>

<template>
  <div class="container">
    <div class="row my-3">
      <h1>Calculadora</h1>
    </div>
    <div class="row">
      <h4 class="my-2">Numero 1:</h4>
      <input
        class="form-control form-control-sm"
        type="number"
        v-model="estado.num1"
      />
      <h4 class="my-2">Numero 2:</h4>
      <input
        class="form-control form-control-sm"
        type="number"
        v-model="estado.num2"
      />
    </div>
    <div class="row">
      <select class="form-select form-select-sm my-3" v-model="estado.operacao">
        <option value="somar">+</option>
        <option value="subtrair">-</option>
        <option value="multiplicar">*</option>
        <option value="dividir">/</option>
      </select>
    </div>
    <div class="row">
      <h4 v-if="estado.resultado !== null">
        Resultado: {{ estado.resultado }}
      </h4>
      <h4 v-else>Insíra numero 1 e numero 2</h4>
    </div>
  </div>
</template>

<style scoped></style>
