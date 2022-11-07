<script setup lang="ts">
import { onMounted, ref } from "vue";
import { format } from "date-fns";
import AutoTyper from "./components/AutoTyper.vue";

const now = () => {
  return format(new Date(), "yyyy-MM-dd HH:mm:ss");
};
const text = ref("");
const refresh = () => {
  setInterval(() => {
    text.value = now();
  }, 1000);
};

onMounted(() => {
  refresh();
});
</script>

<template>
  <main>
    <h1 class="title">shahow.top</h1>
    <p class="typer">
      <span class="wrapper">{</span>
      <AutoTyper :text="text"></AutoTyper>
      <span class="wrapper">}</span>
    </p>
  </main>
  <footer>
    <a href="https://beian.miit.gov.cn/">闽ICP备2022013974号-1</a>
  </footer>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  justify-content: center;

  height: 80vh;
}

main > .title {
  font-size: 88px;
  color: var(--base-color);
}

.typer {
  display: flex;
  flex-direction: row;
  justify-content: center;
  place-items: center;
}

.typer > .wrapper {
  font-size: 20px;
}

footer {
  display: flex;
  align-items: flex-end;

  height: 20vh;
}

footer > a {
  color: var(--base-color);
}
</style>
