
<template>
  <v-app>
    <v-main>
      <v-sheet height="100vh" width="100vw" class="backgroud">
        <v-row justify="center" align="center" style="height : 100vh;">
          <nuxt />
        </v-row>
      </v-sheet>
    </v-main>
  </v-app>
</template>
<script>
export default {
  name: 'LoginVue'
}
</script>
<style scoped>
  .backgroud {
    background-color: antiquewhite;
  }
</style>
