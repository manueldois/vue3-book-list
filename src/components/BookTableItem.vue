<script setup lang="ts">
import { Book } from "../types";

defineProps<{
  book: Book;
  showDescription: boolean;
  isHighlighted: boolean;
}>();

defineEmits<{click: []}>()
</script>

<template>
  <tr :class="{ highlight: isHighlighted }" @click="$emit('click')">
    <td class="book-basics">
      <img :src="book.book_image" alt="Book cover" srcset="" />
      <div>
        <p>
          <b> {{ book.title }} </b>
        </p>
        <p>{{ book.author }}</p>
      </div>
    </td>
    <td>
      {{
        new Date(book.created_date).toLocaleDateString(undefined, {
          year: "numeric",
        })
      }}
    </td>
    <td>#{{ book.rank }}</td>
    <td>
      <a v-for="buyLink in book.buy_links.slice(0, 2)" :href="buyLink.url">
        {{ buyLink.name }}
      </a>
    </td>
  </tr>
  <tr
    :class="{
      highlight: isHighlighted,
      visible: showDescription,
      description: true,
    }"
  >
    <td colspan="4">
      <p>{{ book.description }}</p>
    </td>
  </tr>
</template>

<style scoped lang="scss">
tr {
  &.description {
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

  &:not(.description) {
    cursor: pointer;
  }
  &.highlight {
    background-color: whitesmoke;
  }

  td {
    &.book-basics {
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
    a {
      display: block;
    }
  }
}
</style>
