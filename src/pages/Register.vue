<template>
  <q-page class="row q-mx-lg">
    <form>
      <h4>Registro</h4>

      <q-field class="q-mt-sm" label="Usuario" icon="person">
        <q-input
          v-model="form.username"
          color="secondary"
          @blur="$v.form.username.$touch"
          :error="$v.form.username.$error"
        />
      </q-field>
      <q-field class="q-mt-sm" label="Contraseña" icon="vpn key">
        <q-input
          type="password"
          v-model="form.password"
          color="secondary"
          @blur="$v.form.password.$touch"
          :error="$v.form.password.$error"
        />
      </q-field>
      <q-field class="q-mt-sm" label="Confirmar contraseña" icon="vpn key">
        <q-input
          type="password"
          v-model="form.password_confirmation"
          color="secondary"
          @blur="$v.form.password_confirmation.$touch"
          :error="$v.form.password_confirmation.$error"
        />
      </q-field>
      <div class="text-center">
        <q-btn class="q-mt-md" color="secondary" label="Registrarme" @click="register" />
      </div>
      <div class="text-center">
        <q-btn flat class="q-mt-md" color="secondary" label="Iniciar sesión" @click="$router.push('/login')" />
      </div>
    </form>
  </q-page>
</template>
<script>
import { required, sameAs } from 'vuelidate/lib/validators'

export default {
  name: 'PageLogin',
  data () {
    return {
      form: {
        username: '',
        password: '',
        password_confirmation: ''
      },
      users: []
    }
  },
  created () {
    this.users = this.$q.localStorage.get.item('users')
  },
  validations: {
    form: {
      username: { required },
      password: { required },
      password_confirmation: { required, sameAs: sameAs('password') }
    }
  },
  methods: {
    register () {
      if (this.validationHasErrors()) return

      if (this.userAlreadyExists()) {
        this.$q.notify('Nombre de usuario ya ha sido registrado')
        return
      }

      const newUser = {
        username: this.form.username,
        password: this.form.password
      }

      this.users.push(newUser)
      this.$q.localStorage.set('users', this.users)
      this.$q.localStorage.set('auth-user', newUser)
      this.$root.$emit('logged-in')
      this.$router.push('/')
    },
    validationHasErrors () {
      this.$v.form.$touch()

      return this.$v.form.$error
    },
    userAlreadyExists () {
      return this.users.find(user => user.username === this.form.username)
    }
  }
}
</script>
