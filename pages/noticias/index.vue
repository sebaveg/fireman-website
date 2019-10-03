<template lang="pug">
  v-container
    // Search input to filters restaurants
    //- form
    //-   input(v-model="query" type="search" placeholder="Search...")
    h2.display-1.text-center Últimas noticias
    // Noticias cards
    v-row(justify="center")
      v-col(cols="12" md="6" lg="4" v-for="(noticia,i) in noticiasWithShow" :key="i")
        v-card(max-width="512" style="margin: 0 auto")
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

        // If no noticias have been found
        div(v-if="filteredList.length == 0")
          p No hay noticias encontradas
</template>

<script>
// Import the restaurants query
import noticiasQuery from '@/apollo/queries/noticia/noticias'

export default {
  data() {
    return {
      noticias: [],
      noticiasWithShow: [], // individual expansion card
      query: ''
    }
  },
  computed: {
    // Search system
    filteredList() {
      return this.noticias.filter((noticia) => {
        return noticia.Titulo.toLowerCase().includes(this.query.toLowerCase())
      })
    }
  },
  apollo: {
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
  //       // Initialize an empty restaurants variabkle
  //       carrousels: [],
  //       noticias: [],
  //       query: ''
  //     }
  //   },
  //   apollo: {
  //     carrousels: {
  //       prefetch: true,
  //       query: carrouselQuery
  //     },
  //     noticias: {
  //       prefetch: true,
  //       query: noticiasQuery
  //     }
  //   },
  //     images() {
  //       return this.carrousels[0].Imagenes || []
  //     }
}
</script>
