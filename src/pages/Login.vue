<template>
  <q-page class="row q-mx-lg">
    <form>
      <h4>Iniciar sesión</h4>

      <q-field class="q-mt-sm" label="Usuario" icon="person">
        <q-input
          v-model="username"
          color="secondary"
        />
      </q-field>
      <q-field class="q-mt-sm" label="Contraseña" icon="vpn key">
        <q-input
          type="password"
          v-model="password"
          color="secondary"
        />
      </q-field>
      <div class="text-center">
        <q-btn class="q-mt-md" color="secondary" label="Entrar" @click="login" />
      </div>
      <div class="text-center">
        <q-btn class="q-mt-md" flat color="secondary" label="Registrarse" @click="$router.push('/register')" />
      </div>
    </form>
  </q-page>
</template>
<script>
export default {
  name: 'PageLogin',
  data () {
    return {
      username: '',
      password: '',
      users: []
    }
  },
  created () {
    this.users = this.$q.localStorage.get.item('users')
  },
  methods: {
    login () {
      const authUser = this.users.find(user => user.username === this.username)

      if (authUser) {
        this.$q.localStorage.set('auth-user', authUser)
        this.$root.$emit('logged-in')
        this.$router.push('/')
      } else {
        this.$q.notify('Usuario o contraseña incorrectos')
      }
    }
  }
}
</script>
