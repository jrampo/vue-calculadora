<script setup>
import { reactive } from "vue";

const nome = "qjao";

const objeto = {
  nome: "qejao",
  filmeFavorito: "star wars",
};

function dizOla() {
  return `${nome} diz ola`;
}

const imagemAvatar =
  "https://mundoavatar.com.br/wp-content/uploads/2021/07/avatar-filme.jpeg";
const imagemZuko =
  "https://cdn.pixabay.com/photo/2021/06/22/14/55/zuko-6356391_1280.jpg";

const gostaAvatar = false;
const gostaZuko = false;

const estaAutoriazdo = false;

const estado = reactive({
  contador: 0,
  email: "",
});

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alternaEmail(evento) {
  estado.email = evento.target.value;
}
</script>

<template>
  <h1>{{ dizOla() }}</h1>
  <img v-if="gostaAvatar" :src="imagemAvatar" />
  <img v-else-if="gostaZuko" :src="imagemZuko" />
  <h2 v-else>n gosta de nd</h2>

  <h1 v-if="estaAutoriazdo">liberado chefia</h1>
  <h1 v-else>nao tem nd</h1>

  <button :disabled="false">enviar mensagem</button>

  <br />
  <hr />

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br />
  <hr />

  {{ estado.email }}
  <input type="email" @keyup="alternaEmail" />
</template>

<style scoped>
img {
  max-width: 200px;
}
</style>
