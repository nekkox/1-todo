<script setup>
import ListItem from "@/components/ListItem.vue";
import { ref, onMounted } from "vue";

const listItems = ref([
  { title: "Pizza", checked: true },
  { title: "Ser", checked: false },
  { title: "Szynka", checked: false },
  { title: "Salami", checked: false },
]);

function updateItem(item) {
  const updatedItem = findItemInList(item);
    if(updatedItem){
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
      v-for="(item, index) in listItems"
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
