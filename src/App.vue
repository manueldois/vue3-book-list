<script setup lang="ts">
import { onMounted, ref } from "vue";
import { Book, NYTApiResponse } from "./types";
import BookTableItem from "./components/BookTableItem.vue";
import PaginatedTable from "./components/PaginatedTable.vue";

const bestSellingBooks = ref<Book[]>([]);

onMounted(() => {
  fetch(
    `https://api.nytimes.com/svc/books/v3/lists/overview.json?api-key=${
      import.meta.env.VITE_NYT_API_KEY
    }`
  )
    .then((res) => res.json())
    .then(
      (data: NYTApiResponse) =>
        (bestSellingBooks.value = data.results.lists.flatMap(
          (list) => list.books
        ))
    );
});
</script>

<template>
  <main>
    <h1>Most published books of all time</h1>
    <PaginatedTable :data="bestSellingBooks">
      <template v-slot:header>
        <span>title</span>
        <span>published</span>
        <span>rank</span>
        <span>buy on</span>
      </template>
    </PaginatedTable>
  </main>
</template>

<style scoped></style>
