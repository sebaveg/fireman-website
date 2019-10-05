<template lang="pug">
  v-container
    h2.display-1.text-center.mt-5 Metodos de prevención
    v-row(justify="center")
      v-col(cols="12" md="6" v-for="(prevencion,i) in prevenciones" :key="i")
        v-card(max-width="912" style="margin: 0 auto")
          v-img(v-if="prevencion.imagenes.url" :src="'https://bomberos-brandsen-backend.herokuapp.com' + prevencion.imagenes.url" height="250")
          v-card-title {{ prevencion.titulo }}
          v-card-text
            div(v-html="$md.render(prevencion.descripcion)")
          v-card-actions
            v-btn(color="info" text) Compartir
</template>

<script>
export default {
  name: 'Prevenciones',
  data() {
    return {
      prevenciones: [],
      query: ''
    }
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get(
      'https://bomberos-brandsen-backend.herokuapp.com/prevencions'
    )
    return { prevenciones: data }
  }
}
</script>
