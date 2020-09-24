<template>
  <v-app
    dark
    :style="[
      { backgroundImage: 'url(' + require('../assets/background.svg') + ')' },
      { backgroundSize: '100%' },
      { backgroundRepeat: 'no-repeat' },
      { backgroundPosition: 'center bottom' },
    ]"
  >
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-toolbar light flat>
        <v-btn icon light>
          <v-icon color="grey darken-2">mdi-close</v-icon>
        </v-btn>

        <v-toolbar-title class="grey--text text--darken-4"
          >MENU</v-toolbar-title
        >
      </v-toolbar>
      <v-list class="mt-0">
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
          @click="setTitle(item.title)"
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template v-slot:append>
        <div class="ml-4">
          Version 0.1 <br />
          Todos los derechos reservados
        </div>
      </template>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title class="font-weight-bold" v-text="title" />
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      image: './background.svg',
      items: [
        {
          icon: 'mdi-account',
          title: 'Captura de Datos',
          to: '/',
        },
        {
          icon: 'mdi-account',
          title: 'Mi Perfil',
          to: '/perfil',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: '',
    }
  },
  mounted() {
    this.setTitle(this.items[0].title)
  },
  methods: {
    setTitle(title) {
      this.title = title.toUpperCase()
    },
  },
}
</script>
<style>
.fondo {
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
