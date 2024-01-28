<script setup lang="ts">
import ListItem from "./components/ListItem.vue";
</script>

<template>
  <header>
    <h1><span class="icon" aria-hidden="true">✅</span> To do</h1>
    <p>Building App with Vue.js 3</p>
  </header>

  <ul>
    <ListItem :is-checked="false">This is the slotted content</ListItem>
  </ul>
</template>

<style scoped>
header {
  border-bottom: #333 1px solid;
  background-color: #fff;
}
header::after {
  content: "";
  display: block;
  height: 1px;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.75);
}
h1 {
  font-size: 2rem;
}
h1 .icon {
  font-size: 1rem;
  vertical-align: middle;
}
</style>
