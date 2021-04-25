<template>
  <v-container>
    <v-row
      justify="center"
    >
      <h1>Download</h1>
    </v-row>
    <v-row
      justify="center"
    >
      <p>Something</p>
    </v-row>
    <v-row justify="center">
      <v-btn
        color="primary"
        :disabled="invalid"
        :href="link"
      >
        Download
      </v-btn>
    </v-row>
  </v-container>
</template>

<script>
export default {
  methods: {

  },
  data () {
    return {
      link: (process.env.NODE_ENV === 'production') ? '/api' + this.$route.fullPath : 'http://localhost:3000' + this.$route.fullPath
    }
  },
  async fetch () {
    this.$axios.$get('/find-session/' + this.$route.params.session).catch(e => {
      return this.$nuxt.error({ statusCode: 404 })
    });
  }
}
</script>
