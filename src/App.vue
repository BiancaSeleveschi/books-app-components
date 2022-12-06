<template>
  <div id="app">
    <div>
      <ItemList @delete-book="deleteBook" :show-books="showBook" @show-read-unread-books="showAllBooks"
                name="Books"
                v-bind:class="[showBook ? 'bg-primary text-light' :'bg-secondary rounded-2  w-25 m-auto text-dark']"
                :item-list="books"
      />
    </div>
    <div class="container mt-5">
      <div class="row d-flex justify-content-between">
        <div class="col">
          <ItemList @move-read-unread="moveUnreadBook" @show-read-unread-books="showUnreadBooks"
                    :show-books="isUnreadBooks"
                    name="Unread books"
                    :item-list="unreadBooks"
          />
        </div>
        <div class="col">
          <ItemList @move-read-unread="moveReadBook" @show-read-unread-books="showReadBooks"
                    :show-books="isReadBooks"
                    name="Read books"
                    :item-list="readBooks"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ItemList from "@/components/ItemList";

export default {
  name: 'App',
  components: {
    ItemList,
  },
  data() {
    return {
      books: [
        {title: "Secretele succesului", authorName: "Dale Carnegie", releaseYear: 1936, read: true, readYear: ''},
        {title: "Puterea intentiei", authorName: "Waine Dyer", releaseYear: 2015, read: true, readYear: ''},
        {title: "Mindset", authorName: "Carol S. Dweck", releaseYear: 1987, read: false, readYear: ''},
        {title: "Cand corpul spune nu", authorName: "Gabor Mate", releaseYear: 2018, read: false, readYear: ''},
        {title: "Arta manipularii", authorName: "Kevin Dutton", releaseYear: 2019, read: false, readYear: ''},],
      isReadBooks: true,
      isUnreadBooks: true,
      showBook: false
    }
  },
  computed: {
    unreadBooks() {
      return this.books.filter(book => !book.read)
    },
    readBooks() {
      return this.books.filter(book => book.read)
    }
  },
  methods: {
    moveReadBook(index) {
      this.readBooks[index].read = !this.readBooks[index].read
      this.readBooks.push(this.unreadBooks[index])
      this.unreadBooks.splice(index, 1)
    },
    moveUnreadBook(index) {
      this.unreadBooks[index].read = !this.unreadBooks[index].read
      this.unreadBooks.push(this.readBooks[index])
      this.readBooks.splice(index, 1)
    },
    deleteBook(index) {
      this.books.splice(index, 1)
    },
    showReadBooks() {
    this.isReadBooks = ! this.isReadBooks
    },
    showUnreadBooks() {
    this.isUnreadBooks = !this.isUnreadBooks
    },
    showAllBooks() {
      this.showBook = !this.showBook
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
