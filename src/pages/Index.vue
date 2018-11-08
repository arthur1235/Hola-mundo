<template>
  <q-page class="row flex-center">
    <q-card class="col-5 q-ma-sm" v-for="book in books" :key="book.id" :book="book">
      <q-card-title class="text-center">{{book.id}}</q-card-title>
      <q-card-main>
        <q-card-media>
          <img src="~assets/quasar-logo-full.svg">
        </q-card-media>
      </q-card-main>
      <q-card-actions class="flex-center">
        <q-btn
          @click="openBook(book.id)"
          flat
          :color="book.is_occupied ? 'negative' : 'secondary'"
          label="Seleccionar"
        />
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      books: []
    }
  },
  created () {
    this.books = this.$q.localStorage.get.item('books')
  },
  methods: {
    openBook (id) {
      this.$router.push({
        name: 'book',
        params: { id }
      })
    }
  }
}
</script>
