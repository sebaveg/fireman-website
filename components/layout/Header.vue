<template lang="pug">
  header
    v-system-bar.systembar(color="black" dark window)
      h2.overline Para reportar una emergencia llama al #[strong 100]
    .presentation
      h4.body-1 Bienvenidos a
      br
      h1.display-2.font-weight-bold {{ title }}
    v-navigation-drawer(app disable-resize-watcher fixed v-model="drawer")
      v-list(nav)
        v-list-item(two-line)
          v-list-item-avatar
            img(src="/logo.jpg")
          v-list-item-content
            v-list-item-title Bomberos Voluntarios
            v-list-item-subtitle Menu de navegación
        v-divider
        v-list-item(
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        )
          v-list-item-action
            v-icon(style="font-size: 2rem") {{ item.icon }}
          v-list-item-content
            v-list-item-title(v-text="item.title")
    v-app-bar.appbar(color="#353333" dark elevation="10")
      v-app-bar-nav-icon(class="hidden-md-and-up" @click.stop="drawer = !drawer")
      v-btn(text nuxt to="/noticias") Noticias
      v-btn(text) Prevencion
      v-img.logo(src="logo.jpg" height="100" width="100")
      v-btn(text nuxt to="/about") Sobre nosotros
      v-btn(text) Contacto
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      title: 'Bomberos Voluntarios de Brandsen'
    }
  }
}
</script>

<style scoped>
.appbar,
.systembar,
.presentation {
  display: flex;
  justify-content: center;
}
.presentation {
  background: rgb(177, 16, 16);
  color: #fff;
  flex-wrap: wrap;
  padding: 1.5em 0;
}
.presentation h4 {
  text-align: center;
  width: 100%;
}
.presentation h1 {
  text-shadow: 1px 0 2px #000;
}
.logo {
  border-radius: 50%;
  margin: 0 1rem;
}
</style>
