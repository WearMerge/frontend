<template>
  <v-app>
    <v-app-bar dense flat fixed app class="underline" elevate-on-scroll>
      <v-toolbar-title>
        WearMerge
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <div>
        About
      </div>
      <div>
        Contact
      </div>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <!-- <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer> -->
  </v-app>
</template>

<style>
.underline {
  background: var(--v-primary-base) !important;
  border-bottom: 1px solid rgba(0,0,0,.12)
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
