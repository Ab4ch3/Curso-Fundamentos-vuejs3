<template>
  <h1>Hola {{ name.toLocaleUpperCase() }}</h1>
  <br />
  <div>
    <!-- Uso de v-bind -->
    <h2 v-bind:style="styleblue">Soy Azul</h2>
    <h2 :style="`color: ${arrayColores[1]}`">Soy Mexico</h2>
  </div>
  <br />
  <!-- Usos de If y tenario -->
  <div>
    <p v-if="activo === true">Estoy Activo</p>
    <p v-else-if="activo === false">Estoy Desactivado</p>
    <p v-else>Estoy indeciso</p>
    <br />
    <!-- Ternario -->
    <h2>{{ activo ? "Estoy Activo" : "Estoy Inactivo" }}</h2>
  </div>
  <br />
  <!-- V-for -->
  <div>
    <h2>Listas</h2>
    <ul>
      <li v-for="(colores, index) in arrayColores" :key="index">
        {{ index }}--{{ colores }}
      </li>
    </ul>
    <h2>lista Objeto</h2>
    <ul>
      <li v-for="fruta in objetoFruta" :key="fruta.name">
        {{ fruta }}
      </li>
    </ul>
  </div>
  <!-- Eventos  -->
  <button @click="handleClick">preciona aqui</button>
  <button @click="increment">Aumentar Contador</button>
  <button @click="disminuir">disminuir Contador</button>
  <button @click="resetear">Resetear Contador</button>

  <h1 :class="classCounter">Contador :{{ counter }}</h1>
</template>

<script setup>
import { computed, ref } from "vue";

const name = "Vue Dinamico!!";
const styleblue = "color: blue";
const arrayColores = ["blue", "green", "red"];
const activo = false;
const objetoFruta = {
  name: "Manzana",
  price: "$1.00",
  description: "una manzana",
  id: 1,
};
// Le indicamos al variable que va a ser dinamica y reactiva
const counter = ref(0);

// Cada vez que cambie el valor de counter el ejecutara y devolvera un valor de la clase correspondiente
const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  }
  if (counter.value < 0) {
    return "negative";
  }
});
//Metodos
const handleClick = () => {
  console.log("Me diste Click");
};
const increment = () => {
  console.log("incremento");
  counter.value += 1;
};
const disminuir = () => {
  counter.value -= 1;
};
const resetear = () => {
  counter.value = 0;
};
</script>

<style>
h1 {
  color: red;
}
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: gray;
}
</style>
