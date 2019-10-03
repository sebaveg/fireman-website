<template lang="pug">
  v-container
    h2.display-1.text-center.mt-5 Metodos de prevención
    v-row(justify="center")
      v-col(cols="12" md="6" v-for="(prevencion,i) in prevenciones" :key="i")
        v-card(max-width="912" style="margin: 0 auto")
          v-img(v-if="prevencion.imagenes.url" :src="'http://localhost:1337' + prevencion.imagenes.url" height="250")
          v-card-title {{ prevencion.Titulo }}
          v-card-text
            div(v-html="$md.render(prevencion.descripcion)")
          v-card-actions
            v-btn(color="info" text) Compartir
</template>

<script>
import prevencionesQuery from '@/apollo/queries/prevencion/prevenciones'

export default {
  name: 'Prevenciones',
  data() {
    return {
      prevenciones: [],
      query: ''
    }
  },
  apollo: {
    prevenciones: {
      prefetch: true,
      query: prevencionesQuery
    }
  }
}
</script>
