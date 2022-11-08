<script setup>
import { ref, computed } from "vue";
import Header from "./components/Header.vue";
import Button from "./components/Button.vue";

const amount = ref(10000);
const term = ref(6);
const MIN = 0;
const MAX = 20000;
const STEP = 100;

const formatMoney = computed(() => {
  const formatter = new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
  });

  return formatter.format(amount.value);
});

function handleClickDecrement() {
  const value = amount.value - STEP;

  if (value < MIN) {
    alert("Cantidad no valida");
    return;
  }
  amount.value = value;
}

function handleClickIncrease() {
  const value = amount.value + STEP;

  if (value > MAX) {
    alert("Cantidad no valida");
    return;
  }
  amount.value = value;
}
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />

    <div class="flex justify-between mt-10">
      <Button @fn="handleClickDecrement"> &#8722; </Button>
      <Button @fn="handleClickIncrease"> &#43; </Button>
    </div>

    <div class="my-5">
      <input
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        v-model.number="amount"
      />
      <p class="text-center my-10 text-5xl font-extrabold text-indigo-600">
        {{ formatMoney }}
      </p>

      <h2 class="text-2xl font-extrabold text-gray-500 text-center">
        Elige un <span class="text-indigo-600">plazo</span> a pagar
      </h2>

      <select
        class="w-full p-2 bg-white border border-gray-300 rounded-lg text-center text-xl font-bold text-gray-500 mt-5"
        :value="term"
        v-model.number="term"
      >
        <option value="6">6 meses</option>
        <option value="12">12 meses</option>
        <option value="24">24 meses</option>
      </select>
    </div>
  </div>
</template>
