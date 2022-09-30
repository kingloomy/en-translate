<script setup lang="ts">
import { ref, reactive } from "vue";
import { store } from "../App.vue";

const data : any = ref(null);
const error : any = ref(null);

const options = {
  method: "GET",
  headers: {
    "X-RapidAPI-Key": "x",
    "X-RapidAPI-Host": "deep-translate1.p.rapidapi.com",
  },
};

fetch(
  "https://deep-translate1.p.rapidapi.com/language/translate/v2/languages",
  options
).then((response) => response.json())
  .then((response) => (data.value = response.languages))
  .catch((err) => (error.value = err));
</script>

<template>
  <p class="error" v-if="error">Rate limit reached.</p>
  <label v-else-if="data">
    <h2>Translate to:</h2>
    <select v-model="store.language">
      <option
        v-for="value in data"
        v-bind:key="value"
        :disabled="value.language === 'en'"
      >
        {{ value.language }}
      </option>
    </select>
  </label>
  <p v-else>Loading languages...</p>
</template>

<style scoped>
select {
  border: none;
  padding: 1rem 0;
  width: 100%;
  color: var(--vt-c-text-dark-2);
  background: #111;
  font-family: "Courier New", Courier, monospace;
  transition: 0.1s all;
}
select:is(:hover, :focus) {
  background: #222;
}
.error {
  color: red;
}
</style>
