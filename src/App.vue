<script setup>
import { ref, computed, watch } from "vue";
import Header from "./components/Header.vue";
import Button from "./components/Button.vue";
import { formatMoney, calculateTotalPay } from "./helpers";

const amount = ref(10000);
const term = ref(6);
const total = ref(0);

const MIN = 0;
const MAX = 20000;
const STEP = 100;

watch([amount, term], () => {
  total.value = calculateTotalPay(amount.value, term.value);
});

const monthlyPayment = computed(() => {
  return total.value / term.value;
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
        {{ formatMoney(amount) }}
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

    <div v-if="total" class="my-5 space-y-3 bg-gray-50 p-5">
      <h2 class="text-2xl font-extrabold text-gray-500 text-center">
        Resumen <span class="text-indigo-600">de pagos</span>
      </h2>

      <p class="text-xl text-gray-500 text-center font-bold">
        {{ term }} meses
      </p>
      <p class="text-xl text-gray-500 text-center font-bold">
        {{ formatMoney(total) }} total a pagar
      </p>
      <p class="text-xl text-gray-500 text-center font-bold">
        {{ formatMoney(monthlyPayment) }} mensuales
      </p>
    </div>

    <p v-else class="font-extrabold text-gray-500 text-center">
      A??ade una cantidad y un plazo a pagar
    </p>
  </div>
</template>
