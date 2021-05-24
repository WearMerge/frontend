<template>
  <div>
    <header class="header">
      <v-row justify="center">
        <h1 class="heading h2">ABOUT</h1>
      </v-row>
    </header>
    <section class="section">
      <v-row justify="center">
        <v-col>
          <p>Thesis abstract (comming soon).</p>
        </v-col>
      </v-row>
    </section>
    <header class="header">
      <v-row justify="center">
        <h1 class="heading h2">TEAM</h1>
      </v-row>
    </header>
    <section class="section">
      <v-row justify="center">
        <v-col v-for="(item, i) in team" :key="i" md="3">
          <v-card class="card">
            <v-img contain class="align-end" max-height="200" :src="item.img">
            </v-img>
            <v-card-title>{{ item.name }}</v-card-title>
            <v-card-text>{{ item.text }}</v-card-text>
            <v-card-actions>
              <v-btn v-if="item.github !== ''" icon :href="item.github">
                <v-icon>mdi-github</v-icon>
              </v-btn>
              <v-btn v-if="item.email !== ''" icon :href="item.email">
                <v-icon>mdi-email</v-icon>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      team: [
        {
          img: '/avatar/avatar.png',
          name: 'Athena Vakali',
          text: 'Professor',
          github: '',
          email: 'mailto:avakali@csd.auth.gr',
        },
        {
          img: '/avatar/avatar.png',
          name: 'Sofia Yfantidou',
          text: 'Supervisor',
          github: 'https://github.com/syfantid',
          email: 'mailto:s.yfantidou@gmail.com',
        },
        {
          img: '/avatar/avatar.png',
          name: 'Stefanos Efstathiou',
          text: 'Supervisor',
          github: 'https://github.com/efstathio',
          email: 'mailto:efstathiou.stefanos@gmail.com',
        },
        {
          img: '/avatar/avatar.png',
          name: 'Dimitrios P. Giakatos',
          text: 'Developer',
          github: 'https://github.com/dpgiakatos',
          email: 'mailto:dgiakatos@csd.auth.gr',
        },
      ],
    }
  },
}
</script>

<style>
.header {
  padding-top: 10px;
}
.section {
  padding-top: 92px;
  padding-bottom: 92px;
}
.card {
  width: 300px;
}
</style>
