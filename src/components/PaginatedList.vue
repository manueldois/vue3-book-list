<script setup lang="ts">
import { computed, ref } from "vue";

import rightArrow from "../assets/icons/arrow-right.svg"
import leftArrow from "../assets/icons/arrow-left.svg"


const props = defineProps({
  data: { type: Array<any>, default: [] },
  pageSize: { type: Number, default: 5 },
});

const page = ref(1);

const nPages = computed(() => Math.ceil(props.data.length / props.pageSize));

const goToPage = (nextPage: number) => {
  page.value = nextPage;
};

const paginatedData = computed(() =>
  props.data.slice(
    (page.value - 1) * props.pageSize,
    page.value * props.pageSize
  )
);
</script>

<template>
  <section class="container">
    <slot name="header"></slot>
    <ul>
      <template v-for="(item, i) in paginatedData">
        <slot name="item" :item="item" :i="i + (page - 1) * pageSize"></slot>
      </template>
    </ul>
    <section class="controls">
      <button :disabled="page <= 1" @click="() => goToPage(page - 1)">
        <img :src="leftArrow" alt="Left" srcset="" />
      </button>
      <span class="page"> Page {{ page }} of {{ nPages }} </span>
      <button :disabled="page >= nPages" @click="() => goToPage(page + 1)">
        <img :src="rightArrow" alt="Right" srcset="" />
      </button>
    </section>
  </section>
</template>

<style lang="scss">
section.container {
  padding: 0 20px;
}

ul {
  width: 100%;
  padding: 0;
  margin: 0;
}

section.controls {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: large;
  margin-top: 20px;

  span.page {
    margin: 0 10px;
    font-size: larger;
    translate: 0 -2px;
  }

  button {
    background: none;
    border: none;
    padding: 0;
    margin: 0;
    > img {
      height: 20px;
    }

    &:disabled {
      > img {
        visibility: hidden;
      }
    }
  }
}
</style>
