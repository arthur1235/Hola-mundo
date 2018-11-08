<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-header>
      <q-toolbar
        color="secondary"
      >
        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>
        <template v-if="authUser">
          {{authUser.username}}
          <q-btn flat icon="power_settings_new" @click="logout" />
        </template>
      </q-toolbar>
    </q-layout-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MyLayout',
  data () {
    return {
      authUser: null
    }
  },
  created () {
    this.setAuthUser()

    this.$root.$on('logged-in', () => { this.setAuthUser() })
    this.$root.$on('logged-out', () => { this.setAuthUser() })
  },
  methods: {
    setAuthUser () {
      this.authUser = this.$q.localStorage.get.item('auth-user')
    },
    logout () {
      this.$q.localStorage.remove('auth-user')
      this.$root.$emit('logged-out')
      this.$router.push('/login')
    }
  }
}
</script>

<style>
</style>
