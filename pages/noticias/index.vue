<template lang="pug">
  main
    // Search input to filters restaurants
    form
      input(v-model="query" type="search" placeholder="Search...")

    // Noticias cards
    div(v-for="noticia in noticias")
      div
        //- img(:src="'http://localhost:1337/' + noticia.Imagenes" alt="")
        //-   canvas(width="600" height="400")
        div
          div
            h3 {{ noticia.Title }}
            p {{ noticia.Contenido }}
            // Link to the restaurant using router-link
            //- router-link(:to="{ name: 'restaurants-id', params: { id: restaurant.id }}" tag="a") See dishes

      // If no restaurants have been found
      div(v-if="filteredList.length == 0")
        img(src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800")
      p No restaurants found
</template>

<script>
// Import the restaurants query
import noticiasQuery from '@/apollo/queries/noticia/noticias'

export default {
  data() {
    return {
      // Initialize an empty restaurants variabkle
      noticias: [],
      query: ''
    }
  },
  apollo: {
    noticias: {
      prefetch: true,
      query: noticiasQuery
    }
  },
  computed: {
    // Search system
    filteredList() {
      return this.noticias.filter((noticia) => {
        return noticia.Titulo.toLowerCase().includes(this.query.toLowerCase())
      })
    }
  }
}
</script>
