<script setup lang="ts">
defineProps<{ data: any[] }>();
</script>

<template>
  <section class="paginated-list">
    <slot name="header"></slot>
    <ul>
      <template v-for="(item, i) in data">
        <slot name="item" :item="item" :i="i"></slot>
      </template>
    </ul>
  </section>
</template>

<style lang="scss">
.paginated-list {
  > ul {
    width: 100%;
    padding: 0;
    margin: 0;
  }
}
</style>
