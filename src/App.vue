<script setup>
import { computed, ref } from "vue";

const name = "Vue dinamico";

const counter = ref(0);

const increment = () => {
  counter.value++;
};
const decrememt = () => {
  counter.value--;
};
const reset = () => {
  counter.value = 0;
};

const blockBtn = computed(() => {
  const numSearch = favNumber.value.find((num) => num === counter.value);
  console.log(numSearch);
  // if (numSearch === 0) {
  //   return true;
  // }
  // return numSearch ? true : false;
  return numSearch || numSearch === 0;
});

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
const favNumber = ref([]);

const add = () => {
  favNumber.value.push(counter.value);
};
</script>

<template>
  <div class="container text-center mt-3">
    <h1>{{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Increment</button>
      <button @click="decrememt" class="btn btn-danger">Decrement</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="blockBtn" class="btn btn-primary">
        Add
      </button>
    </div>

    <ul class="list-group mt-4">
      <li
        class="list-group-item"
        v-for="(numero, index) in favNumber"
        :key="index"
      >
        {{ numero }}
      </li>
    </ul>
  </div>
</template>

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
  color: peru;
}
</style>
