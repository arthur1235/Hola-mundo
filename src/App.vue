<template>
  <div id="q-app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
  created () {
    // Creating user

    const users = []

    users.push({
      username: 'arturo',
      password: '123'
    })

    this.$q.localStorage.set('users', users)

    // Creating books

    const books = []

    for (let i = 0; i < 8; i++) {
      books.push({
        id: i + 1,
        is_occupied: false
      })
    }

    this.$q.localStorage.set('books', books)
  }
}
</script>

<style>
</style>
