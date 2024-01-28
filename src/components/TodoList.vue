<script setup>
import ListItem from "@/components/ListItem.vue";
import { ref, computed } from "vue";

const listItems = ref([
  { title: "Szynka", checked: false },
  { title: "Mleko", checked: false },
  { title: "Pizza", checked: true },
  { title: "Ser", checked: false },
  { title: "Salami", checked: false },
]);

const sortedItems = computed(() => {
  return listItems.value.sort((a, b) => a.title.localeCompare(b.title));
});

function updateItem(item) {
  const updatedItem = findItemInList(item);
  if (updatedItem) {
    console.log(updatedItem);
    toggleItemChecked(updatedItem);
  }
}

function findItemInList(item) {
  return listItems.value.find((itemInList) => itemInList.title === item.title);
}

function toggleItemChecked(item) {
  return (item.checked = !item.checked);
}
</script>
<template>
  <ul>
    <li
      v-for="(item, index) in sortedItems"
      :key="index"
      @click="updateItem(item)"
    >
      <ListItem :is-checked="item.checked">{{ item.title }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
}
li {
  margin: 0.4rem 0;
}
</style>
