<template>
  <v-app>
    <v-app-bar dense flat fixed app class="underline" elevate-on-scroll>
      <v-toolbar-title>
        <router-link to="/">
          <v-img
            src="/logo.png"
            max-width="130"
            height="100%"
            alt="WearMerge"
          ></v-img>
        </router-link>
      </v-toolbar-title>
      <v-row no-gutters>
        <v-btn to="/how-it-works" rounded text class="my-2">
          How it works
        </v-btn>
        <v-btn to="/about" rounded text class="my-2"> About </v-btn>
      </v-row>
      <v-spacer></v-spacer>
      <v-btn
        href="https://github.com/WearMerge/backend/issues"
        rounded
        text
        class="my-2"
      >
        Report Bugs
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container class="page">
        <nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <v-container>
        <v-row justify="center">
          <v-col>
            Contact:<br />
            <a href="mailto:wearmerge@outlook.com">
              <strong>wearmerge@outlook.com</strong>
            </a>
          </v-col>
          <v-col align="end">
            This is an <strong>open source</strong> project. Find us on
            <a href="https://github.com/WearMerge/"><strong>GitHub</strong></a>
            .
          </v-col>
        </v-row>
        <v-divider></v-divider>
        <v-container>
          <v-row justify="center">
            <span>
              &copy; {{ new Date().getFullYear() }} - All rights reserved
            </span>
          </v-row>
          <v-row justify="center">
            <span>
              Images from <a href="https://unsplash.com/">Unsplash</a> and <a href="https://pixabay.com/">Pixabay</a>
            </span>
          </v-row>
        </v-container>
      </v-container>
    </v-footer>
  </v-app>
</template>

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

<style>
.underline {
  background: white !important;
  border-bottom: 1px solid rgba(0, 0, 0, 0.12) !important;
}
.page {
  padding-left: 15% !important;
  padding-right: 15% !important;
}
</style>
