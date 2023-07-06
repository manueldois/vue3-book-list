<script setup lang="ts">
import { ref } from "vue";
import { Book } from "../types";

const isExpanded = ref(false);

defineProps<{
  book: Book;
  isHighlighted: boolean;
}>();
</script>

<template>
  <li :class="{ highlight: isHighlighted }" @click="isExpanded = !isExpanded">
    <div class="content">
      <div class="book-basics">
        <img :src="book.book_image" alt="Book cover" srcset="" />
        <div>
          <p>
            <b> {{ book.title }} </b>
          </p>
          <p>{{ book.author }}</p>
        </div>
      </div>
      <span>
        {{
          new Date(book.created_date).toLocaleDateString(undefined, {
            year: "numeric",
          })
        }}
      </span>
      <span>#{{ book.rank }}</span>
      <div>
        <a v-for="buyLink in book.buy_links.slice(0, 2)" :href="buyLink.url">
          {{ buyLink.name }}
        </a>
      </div>
    </div>

    <div class="drawer">
      <p v-if="isExpanded">{{ book.description }}</p>
    </div>
  </li>
</template>

<style scoped lang="scss">
li {
  width: 100%;
  list-style: none;
  cursor: pointer;
  padding: 5px 0;

  &.highlight {
    background-color: whitesmoke;
  }

  div.content {
    display: grid;
    grid-template-columns: 4fr 1fr 1fr 1fr;
    text-align: center;
    a {
      display: block;
    }

    div.book-basics {
      display: flex;
      img {
        width: 100px;
        display: block;
      }

      div {
        display: block;
        margin-left: 20px;
        text-align: left;

        p {
          margin-top: 0;
        }
      }
    }
  }

  div.drawer {
    padding: 10px 20px;
  }
}
</style>
