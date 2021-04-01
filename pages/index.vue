<template>
  <div v-if="display">
    <v-card
      class="form-card"
    >
      <v-container>
        Hello
      </v-container>
    </v-card>
    <v-carousel
      cycle
      hide-delimiters
      height="100vh"
      :show-arrows=false
    >
      <v-carousel-item
        v-for="(slide,i) in slides"
        :key=i
        :src="slide.src"
        class="item"
      >
        <v-row
          class="tag"
          align="end "
          justify="end"
        >
          <v-card
            color="rgba(0,0,0,0.7)"
            elevation="5"
          >
            <v-container>
              Photo by <a :href="slide.photographer.link">{{ slide.photographer.name }}</a> on <a :href="slide.photographer.link">{{ slide.site.name }}</a>
            </v-container>
          </v-card>
        </v-row>
      </v-carousel-item>
    </v-carousel>
  </div>
</template>

<style>
.v-carousel {
  height: calc(100vh - 48px) !important;
}
.tag {
  height: calc(100vh - 48px);
  width: 100%;
}
.form-card {
  position: absolute;
  left: 10%;
  right: 0;
  bottom: 35%;
  padding: 5px;
  width: 20em;
  height: 30em;
  z-index: 1;
}
</style>

<script>
export default {
  methods: {
    onResize() {
      if (window.innerWidth < 1080 && window.innerHeight < 900) {
        this.display = false
      } else {
        this.display = true;
      }
    }
  },
  created () {
    window.addEventListener('resize', this.onResize)
  },
  beforeDestroy () {
    window.addEventListener('resize', this.onResize)
  },
  data () {
    return {
      display: true,
      colors: [
        'indigo',
        'warning',
        'pink darken-2',
        'red lighten-1',
        'deep-purple accent-4',
      ],
      slides: [
        {
          src: '/carousel/1.jpg',
          photographer: {
            name: 'Daniel Frank',
            link: 'https://unsplash.com/@fr3nks'
          },
          site: {
            name: 'Unsplash',
            link: 'https://unsplash.com/'
          }
        },
        {
          src: '/carousel/2.jpg',
          photographer: {
            name: 'Annie Spratt',
            link: 'https://unsplash.com/@anniespratt'
          },
          site: {
            name: 'Unsplash',
            link: 'https://unsplash.com/'
          }
        },
        {
          src: '/carousel/3.jpg',
          photographer: {
            name: 'Ryunosuke Kikuno',
            link: 'https://unsplash.com/@kknrynsk_jp'
          },
          site: {
            name: 'Unsplash',
            link: 'https://unsplash.com/'
          }
        }
      ]
    }
  }
}
</script>
