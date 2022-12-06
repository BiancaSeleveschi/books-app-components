<template>
  <div id="app">
    <div>
      <ItemList @move-read-unread="moveBook"
                @show-read-unread-books="showAllBooks"
                @change-index="changeIndexBook"
                @delete-book="deleteBook"
                :index-book="indexBook"
                :show-books="showBook"
                :item-list="books"
                name="Books"
                v-bind:class="[ !showBook ? 'bg-secondary rounded-2  w-25 m-auto text-dark' :' w-25 mx-auto']"
      />
    </div>
    <div class="container mt-5 ">
      <div class="row d-flex justify-content-between">
        <div class="col  mx-3">
          <ItemList @move-read-unread="moveBook"
                    @delete-book="deleteBook"
                    @show-read-unread-books="showUnreadBooks"
                    @change-index="changeIndexUnreadBook"
                    :show-books="isUnreadBooks"
                    :index-book="indexUnreadBook"
                    :item-list="unreadBooks"
                    name="Unread books"
                    v-bind:class="{'bg-success rounded-2 text-dark mx-auto w-50' : !isUnreadBooks }"
          />
        </div>
        <div class="col">
          <ItemList  @move-read-unread="moveBook"
                    @show-read-unread-books="showReadBooks"
                    @delete-book="deleteBook"
                    @change-index="changeIndexReadBook"
                    :index-book="indexReadBook"
                    :show-books="isReadBooks"
                    :item-list="readBooks"
                    name="Read books"
                    v-bind:class="{'bg-warning rounded-2 mx-auto w-50' : !isReadBooks }"/>
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
      showBook: false,
      indexBook: -1,
      indexReadBook: -1,
      indexUnreadBook: -1
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
    moveBook(index) {
      this.books[index].read = !this.books[index].read
      if (this.books[index].read) {
        this.readBooks.push(this.unreadBooks[index])
        this.unreadBooks.splice(index, 1)
      } else {
        this.unreadBooks.push(this.readBooks[index])
        this.readBooks.splice(index, 1)
      }
    },
    deleteBook(book) {
      let index = this.books.findIndex(b => book.title === b.title)
      this.books.splice(index, 1)
      this.indexReadBook = this.indexUnreadBook = -1
    },
    showReadBooks() {
      this.isReadBooks = !this.isReadBooks
    },
    showUnreadBooks() {
      this.isUnreadBooks = !this.isUnreadBooks
    },
    showAllBooks() {
      this.showBook = !this.showBook
    },
    changeIndexBook(index) {
      this.indexBook = this.indexBook != index ? index : -1
    },
    changeIndexReadBook(index) {
      this.indexReadBook = this.indexReadBook != index ? index : -1
    },
    changeIndexUnreadBook(index) {
      this.indexUnreadBook = this.indexUnreadBook != index ? index : -1
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
  margin-top: 60px
}
</style>
