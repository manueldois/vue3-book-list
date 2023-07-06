<script setup lang="ts">
import { ref } from "vue";
import type { Book } from "../types";
import BookTableItem from "./BookTableItem.vue";
const props = defineProps<{ data: any[] }>();
const openDrawer = ref<number | null>(null);
</script>

<template>
  <section class="paginated-list">
    <div class="header">
      <slot name="header"></slot>
    </div>
    <ul>
      <template v-for="(item, i) in data">
        <BookTableItem
          :book="item"
          :is-highlighted="i % 2 === 0"
          :show-description="openDrawer === i"
          @click="openDrawer !== i ? (openDrawer = i) : (openDrawer = null)"
        ></BookTableItem>
      </template>
    </ul>
  </section>
</template>

<style lang="scss">
.paginated-list {
  > .header {
    display: grid;
    grid-template-columns: 4fr 1fr 1fr 1fr;
    text-align: center;
    text-transform: uppercase;
    color: gray;
    font-weight: bold;

    > *:nth-child(1) {
      text-align: left;
    }
  }

  > ul {
    width: 100%;
    padding: 0;
    margin: 0;
  }
}
</style>
