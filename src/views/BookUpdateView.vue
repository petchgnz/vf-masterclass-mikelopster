<script setup>
import { reactive, onMounted, ref, computed } from 'vue'
import { useRoute, useRouter, RouterLink } from 'vue-router'
import { useBookStore } from '../stores/book'

const route = useRoute()
const router = useRouter()
const bookStore = useBookStore()

const bookData = reactive({
  name: '',
  author: '',
})

const mode = ref('create')
const bookIndex = ref(-1)

onMounted(() => {
  if (route.name === 'book-edit') {
    mode.value = 'update'
    bookIndex.value = parseInt(route.params.id)

    const currentBookStore = bookStore.books[bookIndex.value]
    bookData.name = currentBookStore.name
    bookData.author = currentBookStore.author
  }
})

const addBook = () => {
  if (mode.value === 'update') {
    bookStore.editBook(bookData, bookIndex.value)
  } else {
    bookStore.addBook(bookData)
  }

  router.push({ name: 'book-list' })
}

const displayButton = computed(() => {
  if (mode.value === 'create') {
    return 'Add'
  } else {
    return 'Update'
  }
})
</script>

<template>
  Book Update View
  <div>
    <div>Book name</div>
    <input type="text" v-model="bookData.name" />
  </div>

  <div>
    <div>Book author</div>
    <input type="text" v-model="bookData.author" />
  </div>

  <button @click="addBook">{{ displayButton }} Book</button>
  <RouterLink :to="{ name: 'book-list' }">Back to List</RouterLink>
</template>
