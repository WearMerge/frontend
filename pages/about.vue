<template>
  <v-container>
    <section>
      <v-row justify="center">
        <h1>ABOUT</h1>
      </v-row>
      <v-row justify="center">
        <p>Thesis abstract (comming soon).</p>
      </v-row>
    </section>
    <section>
      <v-row justify="center">
        <h1>Team</h1>
      </v-row>
      <v-row v-for="(item, i) in team" :key="i" justify="center">
        <v-card>
          <v-img contain class="align-end" max-height="200" :src="item.img">
          </v-img>
          <v-card-title>{{ item.name }}</v-card-title>
          <v-card-text>{{ item.text }}</v-card-text>
          <v-card-actions>
            <v-btn icon :href="item.github">
              <v-icon>mdi-github</v-icon>
            </v-btn>
            <v-btn icon :href="item.email">
              <v-icon>mdi-email</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-row>
    </section>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      team: [
        {
          img: '/avatar/avatar1.png',
          name: 'Dimitrios P. Giakatos',
          text: 'Something',
          github: 'https://github.com/dpgiakatos',
          email: 'mailto:dgiakatos@csd.auth.gr',
        },
      ],
    }
  },
}
</script>
