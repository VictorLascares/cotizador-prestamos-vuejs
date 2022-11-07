<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";

const amount = ref(0);
const state = reactive({
  amount: 0,
});

function handleInput(e) {
  state.amount = Number(e.target.value);
}

console.log(amount.value);
console.log(state.amount);
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />

    <div class="my-5">
      <input
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        @input="handleInput"
      />
      {{ state.amount }}
    </div>
  </div>
</template>
