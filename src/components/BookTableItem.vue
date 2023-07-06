<script setup lang="ts">
import { Book } from "../types";

defineProps<{
  book: Book;
  showDescription: boolean;
  isHighlighted: boolean;
}>();

defineEmits<{ click: [] }>();
</script>

<template>
  <li :class="{ highlight: isHighlighted }" @click="$emit('click')">
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
    <div
      :class="{
        highlight: isHighlighted,
        visible: showDescription,
        description: true,
      }"
    >
      <p>{{ book.description }}</p>
    </div>
  </li>
</template>

<style scoped lang="scss">
li {
  width: 100%;
  list-style: none;
  cursor: pointer;
  display: grid;
  grid-template-columns: 4fr 1fr 1fr 1fr;
  padding: 10px 0;
  text-align: center;

  &.highlight {
    background-color: whitesmoke;
  }

  a {
    display: block;
  }

  div.description {
    p {
      height: 0;
      overflow: hidden;
    }
    &.visible {
      p {
        height: fit-content;
      }
    }
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
</style>
