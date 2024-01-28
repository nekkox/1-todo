<script setup>
import ListItem from "@/components/ListItem.vue";
import { ref, computed, onMounted } from "vue";

const storageItems = ref([]);

const setToStorage = (items) => {
  localStorage.setItem("list-items", JSON.stringify(items));
};

const getFromStorage = () => {
  const stored = localStorage.getItem("list-items");
  if (stored) {
    return JSON.parse(stored);
  }
  return [];
};

function initListItems() {
  if (storageItems.value?.length === 0) {
    const listItems = [
      { id: 1, title: "Szynka", checked: false },
      { id: 2, title: "Mleko", checked: false },
      { id: 3, title: "Pizza", checked: true },
      { id: 4, title: "Ser", checked: false },
      { id: 5, title: "Salami", checked: false },
    ];
    setToStorage(listItems);
    storageItems.value = listItems;
  }
}

const sortedItems = computed(() => {
  return listItems.value.sort((a, b) => a.title.localeCompare(b.title));
});

const sortedList = computed(() =>
  [...storageItems.value].sort(
    (a, b) => (a.checked ? 1 : 0) - (b.checked ? 1 : 0)
  )
);

function updateItem(item) {
  const updatedItem = findItemInList(item);
  if (updatedItem) {
    toggleItemChecked(updatedItem);
    setToStorage(storageItems.value);
  }
}

function findItemInList(item) {
  return storageItems.value.find(
    (itemInList) => itemInList.title === item.title
  );
}

function toggleItemChecked(item) {
  return (item.checked = !item.checked);
}

onMounted(() => {
  initListItems();
  storageItems.value = getFromStorage();
});
</script>

<template>
  <hr />
  <ul>
    <li v-for="item in sortedList" :key="item.id" @click="updateItem(item)">
      <ListItem :is-checked="item.checked">{{ item.title }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
}
li {
  margin: 1rem 0;
}
</style>
