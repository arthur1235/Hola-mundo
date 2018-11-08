<template>
  <q-page class="row">
    <q-card class="col-12">
      <q-card-title class="text-center">{{bookId}}</q-card-title>
      <q-card-main>
        <q-card-media>
          <img src="~assets/quasar-logo-full.svg">
        </q-card-media>
      </q-card-main>
      <q-card-actions class="flex-center">
        <q-btn
          :disable="book.is_occupied"
          label="Check in"
          color="secondary"
          @click="setOccupied(true)"
        />
        <q-btn
          :disable="!book.is_occupied"
          label="Check out"
          color="secondary"
          @click="setOccupied(false)"
        />
      </q-card-actions>
    </q-card>
  </q-page>
</template>
<script>
export default {
  name: 'PageBook',
  data () {
    return {
      books: [],
      book: null,
      bookIndex: -1
    }
  },
  created () {
    this.books = this.$q.localStorage.get.item('books')

    this.book = this.books.find(book => book.id === this.bookId)

    this.bookIndex = this.books.findIndex(book => book.id === this.bookId)
  },
  computed: {
    bookId () {
      return this.$route.params.id
    }
  },
  methods: {
    setOccupied (occupied) {
      this.book.is_occupied = occupied

      this.books[this.bookIndex] = this.book

      this.$q.localStorage.set('books', this.books)

      this.$router.push('/')
    }
  }
}
</script>
