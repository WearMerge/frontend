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
      </v-row>
      <v-spacer></v-spacer>
      <v-btn href="https://github.com/WearMerge/backend/issues" rounded text class="my-2">
        Report Bugs
      </v-btn>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <v-footer :absolute="!fixed" app>
      <v-container>
        <v-row justify="center">
          <v-col>
            Contact:<br>
            <a href="mailto:wearmerge@outlook.com"><strong>wearmerge@outlook.com</strong></a>
          </v-col>
          <v-col align="end">
            This is an <strong>open source</strong> project. Find us on <a href="https://github.com/WearMerge/"><strong>GitHub</strong></a>.
          </v-col>
        </v-row>
        <v-divider></v-divider>
        <v-container>
          <v-row justify="center">
            <span>&copy; {{ new Date().getFullYear() }} - All rights reserved</span>
          </v-row>
          <v-row justify="center">
            <span>Images from <a href="https://unsplash.com/">Unsplash</a></span>
          </v-row>
        </v-container>
      </v-container>
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
