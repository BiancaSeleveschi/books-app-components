<template>
  <div>
    <h1 @click="showReadUnreadBooks">{{ name }}</h1>
    <ul v-show="showBooks" class="list-unstyled">
      <li v-for="(book, index) in itemList" v-bind:key="index"
          class="border rounded-4 bg-warning p-3 my-4 w-25 mx-auto">
        <h2>{{ book.title }}</h2>
        <h4>Author name: {{ book.authorName }}</h4>
        <p>Release year: {{ book.releaseYear }}</p>
        <button @click="moveReadOrUnread(index)"
                class='mx-3'
                v-bind:class="[book.read ? 'btn btn-success' : 'btn btn-primary']">
          {{ book.read ? 'Unread' : 'Read' }}
        </button>
        <button @click="deleteBook" class="btn btn-danger">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ItemList",
  props: ['itemList', 'name', 'showBooks'],
  methods: {
    showReadUnreadBooks() {
      this.$emit('show-read-unread-books')
    },
    moveReadOrUnread(index) {
      this.$emit('move-read-unread', index)
    },
    deleteBook(index) {
      this.$emit('delete-book', index)
    },
  }
}
</script>

<style scoped>

</style>