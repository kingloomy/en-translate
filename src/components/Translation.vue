<script setup lang="ts">
import { ref, reactive } from "vue";
import { store } from "../App.vue";

const data : any = ref(null);
const error : any = ref(null);
const fetchStatus = ref(false);

function getTranslation() {
  error.value = null;
  
const options = {
	method: 'POST',
	headers: {
		'content-type': 'application/json',
		'X-RapidAPI-Key': '5ff71a972amsha91b71a64759e71p1982f1jsn3e63dfe04a5f',
		'X-RapidAPI-Host': 'deep-translate1.p.rapidapi.com'
	},
	body: `{"q":"${store.source}","source":"en","target":"${store.language}"}`
};

fetch('https://deep-translate1.p.rapidapi.com/language/translate/v2', options)
    .then((response) => response.json())
    .then((response) => (data.value = response.data))
    .catch((err) => (error.value = err));

    console.log(data)
  fetchStatus.value = true;
}
</script>

<template>
  <div>
    <h2>Original Text:</h2>
    <textarea
      v-model="store.source"
      placeholder="Enter a phrase to be translated."
    /><br />
    <button @click="getTranslation" :disabled="store.source === ''">
      Translate
    </button>
    <div v-if="fetchStatus">
      <p v-if="error">Error occurred: {{ error.message }}</p>
      <div class="translate-cont" v-else-if="data">
        <h2>Translated Text</h2>
        <p>
          {{ data.translations.translatedText }}
        </p>
      </div>
      <p v-else>Loading...</p>
    </div>
  </div>
</template>

<style scoped>
  textarea{
    resize: none;
    border: none;
    padding: 1rem;
    width: 100%;
    min-height: 10em;
    color: var(--vt-c-text-dark-2);
    background: #111;
    font-family: "Courier New", Courier, monospace;
    transition: .1s all;
  }

  textarea:is(:hover, :focus){
    background: #222;
  }

  button{
    border: none;
    width: 100%;
    height: 2em;
    color: var(--vt-c-text-dark-2);
    background: #111;
    transition: .1s all;
  }

  button:is(:hover, :focus-visible){
    background: #222;
  }

  button:active{
    background: #333;
  }

  .translate-cont{
    margin: 1rem 0rem;
    padding: 1rem;
    background: #111;
  }
</style>