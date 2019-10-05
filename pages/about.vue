<template lang="pug">
  v-container
    v-row(justify="center")
      v-col(cols="12")
        h1.text-center.my-5 {{ historias[0].titulo }}
        figure
          v-img(:src="'https://bomberos-brandsen-backend.herokuapp.com/'+historias[0].imagen.url")
        div.mt-5(v-html="$md.render(historias[0].descripcion || 'No se ha escrito una historia')")
</template>

<script>
export default {
  data() {
    return {
      historias: [],
      query: ''
    }
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get(
      'https://bomberos-brandsen-backend.herokuapp.com/historias'
    )
    return { historias: data }
  }
}
</script>
