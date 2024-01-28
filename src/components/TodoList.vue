<script setup>
    import ListItem from "@/components/ListItem.vue";
  
</script>
<template>
     <ul>
        <ListItem :is-checked="false">This is the slotted content</ListItem>
      </ul>
</template>