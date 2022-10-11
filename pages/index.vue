<template>
  <LoginVue />
</template>

<script>
import LoginVue from '~/components/users/LoginVue.vue'
export default {
  name: 'IndexPage',
  components: { LoginVue },
  auth: false,
  layout: 'LoginVue'
}
</script>
