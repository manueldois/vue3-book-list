<script setup lang="ts">
import { ref } from "vue";
import type { Book } from "../types";
import BookTableItem from "./BookTableItem.vue";
const props = defineProps<{ data: any[] }>();
const openDrawer = ref<number | null>(null);
</script>

<template>
  <table>
    <slot name="header"></slot>
    
    <template v-for="(item, i) in data">
      <BookTableItem
        :book="item"
        :is-highlighted="i % 2 === 0"
        :show-description="openDrawer === i"
        @click="openDrawer !== i ? (openDrawer = i) : (openDrawer = null)"
      ></BookTableItem>
    </template>
  </table>
</template>

<style scoped lang="scss">
table {
  width: 100%;
  border-spacing: 0;

  th {
    text-align: left;
    text-transform: uppercase;
    color: gray;
  }
}
</style>
