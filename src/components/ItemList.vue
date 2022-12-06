<template>
  <div class="rounded-1">
    <h1 @click="showReadUnreadBooks">{{ name }}</h1>
    <ul v-show="showBooks" class="list-unstyled">
      <li v-for="(book, index) in itemList" v-bind:key="index"
          class="border rounded-4 p-3 my-4 mx-auto "
          v-bind:class="[book.read ? 'bg-warning' : 'bg-success text-dark']">
        <h2 @click="changeIndex(index)">{{ book.title }}</h2>
        <div v-show="indexBook === index">
        <h4>Author name: {{ book.authorName }}</h4>
        <p>Release year: {{ book.releaseYear }}</p>
        <button @click="moveReadOrUnread(index)"
                class='mx-3'
                v-bind:class="[book.read ? 'btn btn-success' : 'btn btn-primary']">
          {{ book.read ? 'Unread' : 'Read' }}
        </button>
        <button @click="deleteBook(book)" class="btn btn-danger">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ItemList",
  props: ['itemList', 'name', 'showBooks', 'indexBook'],
  methods: {
    showReadUnreadBooks() {
      this.$emit('show-read-unread-books')
    },
    moveReadOrUnread(index) {
      this.$emit('move-read-unread', index)
    },
    deleteBook(book) {
      this.$emit('delete-book', book)
    },
    changeIndex(index) {
      this.$emit('change-index', index)
    }
  }
}
</script>

<style scoped>

</style>