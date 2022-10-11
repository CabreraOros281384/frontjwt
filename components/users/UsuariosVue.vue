<template>
  <v-row class="renglon">
    <v-col cols="12">
      <v-card color="cyan" elevation="6">
        <v-card-title>
          Usuarios
        </v-card-title>
        <v-card-text>
          <v-row
            v-for="(item, index) in usuarios"
            :key="index"
          >
            <v-tooltip bottom>
              <template #activador="{ on, attrs }">
                <p
                  v-bind="attrs"
                  v-on="on"
                >
                  {{ item.name }} - {{ item.email }} - {{ item.date }}
                </p>
              </template>
              <span>Tooltip nuevo</span>
            </v-tooltip>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data () {
    return {
      usuarios: []
    }
  },
  created () {
    this.ObtenerUsuarios()
  },
  methods: {
    async ObtenerUsuarios () {
      const headers = {
        'Content-Type': 'application/json; charset=UTF-8',
        'Access-Control-Allow-Origin': '*'
      }
      await this.$axios.get('/users/all',
        { headers }
      ).then((res) => {
        this.usuarios = res.data.data
      }).catch((error) => {
        console.log(error)
      })
    }
  }
}

</script>
