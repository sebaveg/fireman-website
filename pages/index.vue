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
      h2.display-2.text-center.mt-5 Últimas noticias
      // Noticias cards
      v-row(justify="center")
        v-col(cols="12" md="6" lg="4" v-for="(noticia,i) in noticiasWithShow" :key="i")
          v-card(max-width="512" style="margin: 0 auto" elevation="7")
            v-img(v-if="noticia.Imagenes[0]" :src="'http://localhost:1337' + noticia.Imagenes[0].url" height="250")
            v-card-title {{ noticia.Titulo }}
            v-card-actions
              v-btn(text) Compartir
              .flex-grow-1
              v-btn(icon @click="noticia.show = !noticia.show")
                v-icon {{ noticia.show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}
            //- img(:src= alt="")
            //-   canvas(width="600" height="400")
            v-expand-transition
              div(v-show="noticia.show")
                v-card-text {{ noticia.Descripcion }}
</template>

<script>
// Importa las fotos de la portada del carrusel
import carouselsQuery from '@/apollo/queries/carousels'
import noticiasQuery from '@/apollo/queries/noticia/noticias'

export default {
  data() {
    return {
      carousels: [],
      noticias: [],
      noticiasWithShow: [], // individual expansion card
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
    },
    noticias: {
      prefetch: true,
      query: noticiasQuery
    }
  },
  mounted() {
    this.addShow()
  },
  methods: {
    addShow() {
      this.noticiasWithShow = this.noticias.map((card) => ({
        ...card,
        show: false
      }))
    }
  }
}
</script>
