<script setup lang="ts">
import { onMounted, ref } from "vue";
import { Book, NYTApiResponse } from "./types";
import BookListItem from "./components/BookListItem.vue";
import BookListHeader from "./components/BookListHeader.vue";
import PaginatedList from "./components/PaginatedList.vue";

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
    <PaginatedList :data="bestSellingBooks">
      <template v-slot:header>
        <BookListHeader></BookListHeader>
      </template>
      <template v-slot:item="itemProps">
        <BookListItem
          :book="itemProps.item"
          :is-highlighted="itemProps.i % 2 === 0"
        ></BookListItem>
      </template>
    </PaginatedList>
  </main>
</template>

<style scoped></style>
