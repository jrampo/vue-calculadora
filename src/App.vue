<script setup>
import { reactive, computed } from "vue";

const objeto = {
  nome: "qejao",
  filmeFavorito: "avatarrr",
};

const imagemAvatar =
  "https://mundoavatar.com.br/wp-content/uploads/2021/07/avatar-filme.jpeg";
const imagemZuko =
  "https://cdn.pixabay.com/photo/2021/06/22/14/55/zuko-6356391_1280.jpg";

const gostaAvatar = false;
const gostaZuko = true;

const estaAutoriazdo = false;

const estado = reactive({
  contador: 0,
  palavra: "",
  teste: "",
  nome: "",
  saldo: 5000,
  transferindo: 0,
});

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

//

function inserePalavra(evento) {
  estado.palavra = evento.target.value;
}

function teste(evento) {
  estado.teste = evento.target.value;
}

function alteraNome(evento) {
  estado.nome = evento.target.value;
}

const mandaSalve = computed(() => `Salve guerreiro ${estado.nome}`);

function mostraSaldoFuturo() {
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorTransferencia() {
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}
</script>

<template>
  <img v-if="gostaAvatar" :src="imagemAvatar" />
  <img v-else-if="gostaZuko" :src="imagemZuko" />
  <h2 v-else>n gosta de nd</h2>

  <h1 v-if="estaAutoriazdo">liberado chefia</h1>
  <h1 v-else>foi barrado</h1>

  <button :disabled="false">enviar mensagem</button>

  <br />
  <hr />

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br />
  <hr />

  {{ estado.palavra }}
  <input type="email" @keyup="inserePalavra" />

  {{ estado.teste }}
  <input type="number" @keyup="teste" />

  {{ mandaSalve }}
  <input type="text" @keyup="alteraNome" />

  <br />
  <hr />
  Saldo: {{ estado.saldo }} <br />
  Transferindo: {{ estado.transferindo }} <br />
  Saldo depois da transferencia: {{ mostraSaldoFuturo() }} <br />
  <input
    class="campo"
    :class="{ invalido: !validaValorTransferencia() }"
    @keyup="(evento) => (estado.transferindo = evento.target.value)"
    type="number"
    placeholder="quantia de transferencia"
  />
  <button v-if="validaValorTransferencia()">transferir</button>
  <span v-else>valor maior q o saldo</span>
</template>

<style scoped>
.invalido {
  outline-color: red;
  border-color: red;
}

img {
  max-width: 200px;
}

input {
  width: 160px;
}

.campo {
  border: 2px solid green;
}
</style>
