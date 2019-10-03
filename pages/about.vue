<template lang="pug">
  v-container
    v-row(justify="center")
      v-col(cols="12")
        h1.text-center.my-5 {{ historias[0].titulo }}
        figure
          v-img(:src="'http://localhost:1337/'+historias[0].imagenes[0].url")
        div.mt-5(v-html="$md.render(historias[0].historia || 'No se ha escrito una historia')")
</template>

<script>
import historiasQuery from '@/apollo/queries/historia'

export default {
  data() {
    return {
      historias: [],
      query: ''
    }
  },
  apollo: {
    historias: {
      prefetch: true,
      query: historiasQuery
    }
  }
}
</script>
