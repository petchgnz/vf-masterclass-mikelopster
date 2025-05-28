<script setup>
import { useBookStore } from '../stores/book'
import { RouterLink, useRouter } from 'vue-router'

const bookStore = useBookStore()

const deleteBook = (bookIndex) => {
  bookStore.removeBook(bookIndex)
}
</script>

<template>
  <div>BookListView</div>
  <RouterLink :to="{ name: 'book-create' }">Create book</RouterLink>

  <hr />

  <ul>
    <li v-for="(book, index) in bookStore.books">
      {{ book.name }} - {{ book.author }}

      <RouterLink
        :to="{
          name: 'book-edit',
          params: { id: index },
        }"
        ><button>Edit</button>
      </RouterLink>

      <button @click="deleteBook(index)">Delete</button>
    </li>
  </ul>
</template>
