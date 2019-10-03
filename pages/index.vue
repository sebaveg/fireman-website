<template lang="pug">
  main
    v-carousel(v-if="images" cycle interval="5000")
      v-carousel-item(
        v-for="(image, i) in images"
        :key="i"
      )
        v-parallax(:src="'http://localhost:1337'+image.url" height="700")
    v-container
      v-alert(type="error") En presencia de humo, camina lo mas agachado posible por debajo del mismo y siempre que sea posible, cubriéndote las vías respiratorias con un trapo o un pañuelo húmedo.
</template>

<script>
// Importa las fotos de la portada del carrusel
import carouselsQuery from '@/apollo/queries/carousels'

export default {
  data() {
    return {
      carousels: [],
      query: ''
    }
  },
  computed: {
    images() {
      return this.carousels[0].Imagenes || []
    }
  },
  apollo: {
    carousels: {
      prefetch: true,
      query: carouselsQuery
    }
  }
}
</script>
