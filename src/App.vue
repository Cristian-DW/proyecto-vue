<script setup>
import { onDeactivated, toValue } from "vue";
import { ref, computed } from "vue";

// Reactividad en vue

const y = ref(0);
const arrayFavorito = ref([]);

const increment = () => {
  y.value++;
};
const decrement = () => {
  y.value--;
};
const reset = () => {
  y.value = 0;
};
const add = () => {
  arrayFavorito.value.push(y.value);
};

//  Propiedad computed
const blockAdd = computed(() => {
  const searchNum = arrayFavorito.value.find((num) => num === y.value);
  if (searchNum === 0) return true;
  return searchNum ? true : false;
});

const clases = computed(() => {
  if (y.value === 0) {
    return "zero";
  }
  if (y.value > 0) {
    return "positive";
  }
  if (y.value < 0) {
    return "negative";
  }
});
</script>

<template>
  <div class="container text-center mt-5">
    <h1>Hola, crack</h1>
    <!-- Reactividad en vue  -->
    <h2 :class="clases">{{ y }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuye</button>
      <button @click="reset" class="btn btn-secondary">Restablecer</button>
      <button @click="add" :disabled="blockAdd" class="btn btn-primary">Add</button>
    </div>
    <h2 class="mt-3">Favoritos</h2>
    <ul class=" list-group mt-2">
      <li v-for="favorito in arrayFavorito" :key="favorito" class="list-group-item" >{{ favorito }}</li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: #00000080;
}
.positive {
  color: rgb(28, 218, 28);
}
.negative {
  color: red;
}
.zero {
  color: blue;
}
</style>