<template lang="pug">
  main
    v-carousel(v-if="carousels" cycle interval="5000")
      v-carousel-item(
        v-for="(item, i) in carousels"
        :key="i"
      )
        v-parallax(:src="'https://bomberos-brandsen-backend.herokuapp.com'+item.imagen.url" height="700")
    v-container
      v-alert(type="error") En presencia de humo, camina lo mas agachado posible por debajo del mismo y siempre que sea posible, cubriéndote las vías respiratorias con un trapo o un pañuelo húmedo.
</template>

<script>
// Importa las fotos de la portada del carrusel

export default {
  data() {
    return {
      noticiasWithShow: [], // individual expansion card
      query: ''
    }
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get(
      'https://bomberos-brandsen-backend.herokuapp.com/carousels'
    )
    return {
      carousels: data
    }
  }
}
</script>
