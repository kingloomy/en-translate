<script setup lang="ts">
import { reactive } from "vue";
import Languages from "./components/Languages.vue";
import Translation from "./components/Translation.vue";
</script>

<script lang="ts">
export const store = reactive({
  language: "ja",
  source: "",
});
</script>

<template>
  <div id="stem">
    <header></header>
    <main>
      <section class="form-grid">
        <h1>English Translator</h1>
        <Languages />
        <Translation />
      </section>
      <h3 class="gray">this translate api is very slow lol</h3>
    </main>
  </div>
</template>

<style scoped>
#stem {
  width: 100%;
  font-family: 'Courier New', Courier, monospace;
}
h1 {
  text-decoration: underline;
}
.form-grid {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: clamp(1rem, 5%, 5rem);
}
.gray{
  width: 100%;
  text-align: center;
  opacity: .25;
}
</style>
