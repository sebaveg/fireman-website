<template lang="pug">
  v-app
    FireHeader
    v-content
      nuxt
    FireFooter
</template>

<script>
import FireHeader from '../components/layout/Header'
import FireFooter from '../components/layout/Footer'
export default {
  name: 'Default',
  components: { FireHeader, FireFooter },
  data() {
    return {}
  }
}
</script>
