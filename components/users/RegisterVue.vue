<template>
  <v-row class="renglon">
    <v-col cols="6">
      <v-form ref="form" v-model="valid">
        <v-card>
          <v-card-title>
            Registro de usuarios
          </v-card-title>
          <v-card-text>
            <v-text-field
              v-model="user"
              type="text"
              placeholder="Escribe el nombre del usuario"
              label="Usuario"
            />
            <v-text-field
              v-model="mail"
              type="mail"
              :rules="emailRule"
              placeholder="Escribe el correo del usuario"
              label="Correo Electronico"
            />
            <v-text-field
              v-model="password1"
              type="password"
              :rules="LongPassword"
              placeholder="Escribe la constraseña"
              label="Password"
            />
            <v-text-field
              v-model="password2"
              type="password"
              :rules="matchingPasswords"
              placeholder="Verifica la constraseña"
              label="Verifique el Password"
            />
          </v-card-text>
          <v-card-actions>
            <v-btn
              color="green"
              @click="registraUsuario"
            >
              Registrar
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-form>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data () {
    return {
      valid: false,
      user: null,
      mail: null,
      password1: null,
      password2: null,
      emailRule: [v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'],
      LongPassword: [
        (v) => {
          if (!v || v.length < 6) {
            return 'Longitud Invalida'
          }
          return true
        }
      ],
      matchingPasswords: [
        () => {
          if (this.password1 === this.password2) {
            return true
          } else {
            return 'Las contraseñas no son iguales'
          }
        }
      ]
    }
  },
  methods: {
    async registraUsuario () {
      this.valid = this.$refs.form.validate()
      if (this.valid) {
        const headers = {
          'Content-Type': 'application/json; charset=UTF-8',
          'Acces-Control-Allow-Origin': '*'
        }
        const data = {
          name: this.user,
          email: this.mail,
          password: this.password1
        }
        await this.$axios.post('/user/register',
          data,
          { headers }
        ).then((res) => {
          console.log(res)
        }).catch((error) => {
          console.log(error)
        })
      } else {
        console.log('invalid')
      }
    }
  }
}

</script>

<style scoped>
    .renglon {
        width: 100%;
        height: 100%;
        padding: 0;
        background-color: darksalmon;

    }
</style>
