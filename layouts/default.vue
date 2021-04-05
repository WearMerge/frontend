<template>
  <v-app>
    <v-app-bar dense flat fixed app class="underline" elevate-on-scroll>
      <v-toolbar-title>
        <NuxtLink to="/">
          WearMerge
        </NuxtLink>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-col cols="auto">
        <NuxtLink to="/about">
          About
        </NuxtLink>
      </v-col>
      <v-col cols="auto" >
        <NuxtLink to="/contact">
          Contact
        </NuxtLink>
      </v-col>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <v-footer
      v-if="$route.name !== '/'"
      :absolute="!fixed"
      app
    >
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
