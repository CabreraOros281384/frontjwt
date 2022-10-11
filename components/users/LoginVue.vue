<template>
  <v-card
    elevation="2"
    width="500"
    color="blue"
    style="display: flex;"
  >
    <v-col cols="4" style=" align-self: center;">
      <v-img :src="require('~/assets/imagenes/loging.jpg')" />
    </v-col>
    <v-col>
      <v-card-title>Login Proyecto </v-card-title>
      <v-card-text>
        <v-text-field
          v-model="email"
          type="mail"
          :rules="emailRule"
          placeholder="Escribe tu correo"
        />
        <v-text-field v-model="password" type="password" placeholder="Escribe tu contraseña" />
      </v-card-text>
      <v-card-actions>
        <v-btn
          color="brown"
          @click="login"
        >
          Login
        </v-btn>
        <v-btn>
          Cancel
        </v-btn>
      </v-card-actions>
    </v-col>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      email: null,
      password: null,
      emailRule: [v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'

      ]
    }
  },
  methods: {
    async login () {
      const user = {
        email: this.email,
        password: this.password
      }
      await this.$auth.loginWith('local', {
        data: user
      }).then((res) => {
        this.$router.push('/dashboard')
      }).catch((error) => {
        console.log('error', error)
      })
    }
  }
}
</script>
