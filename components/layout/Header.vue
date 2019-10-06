<template lang="pug">
  header
    v-system-bar.systembar(color="black" dark window)
      h2.overline Para reportar una emergencia llama al #[strong 100]
    .presentation
      h4.body-1 Bienvenidos a
      br
      h1.display-2.font-weight-bold.text-center(:class="{'display-1': $vuetify.breakpoint.xs}") {{ title }}
    v-navigation-drawer(app disable-resize-watcher fixed v-model="drawer").navigation-style
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
      v-toolbar-items.appbar(class="hidden-sm-and-down")
        v-btn(text nuxt to="/index") Home
        v-btn(text nuxt to="/noticias") Noticias
        v-btn(text nuxt to="/prevencion") Prevencion
        nuxt-link(to="/"): v-img.logo(src="logo.jpg" height="125" width="125")
        v-btn(text nuxt to="/about") Historia
        v-btn(text nuxt to="/contacto") Contacto
      v-spacer(class="hidden-md-and-up")
      nuxt-link(class="hidden-md-and-up" to="/"): v-img.logo(src="logo.jpg" height="75" width="75")
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      drawer: false,
      items: [
        {
          icon: 'mdi-home',
          title: 'Home',
          to: '/index'
        },
        {
          icon: 'mdi-newspaper',
          title: 'Noticias',
          to: '/noticias'
        },
        {
          icon: 'mdi-shield-alert-outline',
          title: 'Prevencion',
          to: '/prevencion'
        },
        {
          icon: 'mdi-information',
          title: 'Historia',
          to: '/about'
        },
        {
          icon: 'mdi-account-box',
          title: 'Contacto',
          to: '/contacto'
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
  align-items: center;
  position: relative;
  z-index: 10;
}
.presentation {
  background-color: rgb(177, 16, 16);
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
  position: relative;
  z-index: 10;
}
.navigation-style {
  position: absolute;
  z-index: 20;
}
</style>
