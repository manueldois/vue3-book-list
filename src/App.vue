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
    <article class="most-popular-books">
      <h2>Most Popular Books Of All Time</h2>
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
    </article>
  </main>
</template>

<style scoped lang="scss">
.most-popular-books {
  h2 {
    margin-left: 50px;
  }
}
</style>
