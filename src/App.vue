<script setup>
import { ref, computed } from "vue";
import Header from "./components/Header.vue";

const amount = ref(10000);
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
      <button
        class="h-10 w-10 items-center justify-center font-bold bg-lime-500 rounded-full hover:outline-none hover:ring-2 hover:ring-offset-2 hover:ring-lime-500 text-white text-2xl"
        @click="handleClickDecrement"
      >
        &#8722;
      </button>
      <button
        class="h-10 w-10 items-center justify-center font-bold bg-lime-500 rounded-full hover:outline-none hover:ring-2 hover:ring-offset-2 hover:ring-lime-500 text-white text-2xl"
        @click="handleClickIncrease"
      >
        &#43;
      </button>
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
    </div>
  </div>
</template>
