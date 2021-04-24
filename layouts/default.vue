<template>
  <v-app>
    <v-app-bar dense flat fixed app class="underline" elevate-on-scroll>
      <v-toolbar-title>
        WearMerge
      </v-toolbar-title>
      <v-row no-gutters>
        <v-btn to="/how-it-works" rounded text class="my-2">
          How it works
        </v-btn>
        <v-btn to="/about" rounded text class="my-2">
          About
        </v-btn>
        <v-btn to="/contact" rounded text class="my-2">
          Contact
        </v-btn>
      </v-row>
      <v-spacer></v-spacer>
      <v-btn to="/" rounded text class="my-2">
        Report Bugs
      </v-btn>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<style>
.underline {
  background: white !important;
  border-bottom: 1px solid rgba(0,0,0,.12) !important;
}
.page {
  padding: 0;
  margin: 0;
  flex-direction: column;
}
</style>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
    }
  },
}
</script>
