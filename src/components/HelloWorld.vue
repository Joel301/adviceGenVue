<script setup>
import { onMounted, ref } from "vue";

let advice = ref("");
const error = ref(null);

function getAdvice() {
  fetch("https://api.adviceslip.com/advice")
    .then((response) => response.json())
    .then((data) => {
      // advice.value = { ...data.slip };
      console.log(data.slip.advice);
      advice.value = data.slip.advice;
    })
    .catch((err) => {
      console.log(err);
      error.value = err;
    });
}

onMounted(() => {
  getAdvice();
});
</script>

<template>
  <h1>{{ msg }}</h1>
  <!-- {{ advice.value ? advice.value.slip.id : "" }} -->
  <div>
    {{ advice ? advice : "" }}
  </div>
  <button
    @click="
      () => {
        getAdvice();
      }
    "
  >
    imabutton
  </button>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
