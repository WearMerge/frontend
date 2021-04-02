<template>
  <div
    class="main-body"
  >
    <div
      class="form-card"
    >
      <v-card>
        <v-container>
          <v-form
            v-model="valid"
          >
            <v-container>
              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
                required
                outlined
              >
              </v-text-field>
              <template>
                <div
                  v-if="!files.length"
                >
                  <v-file-input
                    v-model="newFiles"
                    outlined
                    multiple
                    prepend-icon=""
                    label="Add Folder"
                    placeholder="Select a folder"
                    webkitdirectory
                    v-on:change="onAdd"
                  >
                  </v-file-input>
                </div>
                <div
                  v-else
                >
                  <v-toolbar
                    flat
                  >
                    <v-toolbar-title>
                      Selected file(s)
                    </v-toolbar-title>
                    <v-divider
                      class="mx-4"
                      inset
                      vertical
                    ></v-divider>
                    <v-spacer></v-spacer>
                    <div
                      align="end"
                    >
                      <v-tooltip
                        bottom
                      >
                        <template v-slot:activator="{ on }">
                          <v-file-input
                            v-model="newFiles"
                            multiple
                            hide-input
                            prepend-icon="mdi-paperclip"
                            webkitdirectory
                            v-on:change="onAdd"
                            v-on:click:clear="onClear"
                            v-on:mouseenter.native="on.mouseenter"
                            v-on:mouseleave.native="on.mouseleave"
                          >
                          </v-file-input>
                        </template>
                        <span>Add Folder</span>
                      </v-tooltip>
                    </div>
                    <v-tooltip
                        bottom
                      >
                        <template v-slot:activator="{ on }">
                          <v-icon
                            v-on:click="onClear"
                            v-on:mouseenter.native="on.mouseenter"
                            v-on:mouseleave.native="on.mouseleave"
                          >
                            mdi-window-close
                          </v-icon>
                        </template>
                      <span>Clear</span>
                    </v-tooltip>
                  </v-toolbar>
                  <v-data-table
                    v-if="files.length"
                    :headers="[{text: 'Name', value: 'name'}]"
                    :items="files"
                    :items-per-page="5"
                    :footer-props="{ disableItemsPerPage: true }"
                  >
                    <template v-for="file in files" v-slot:[`item.${file.value}`]="{ item }">
                      <td :key="file.value">{{ item.name }}</td>
                    </template>
                  </v-data-table>
                </div>
              </template>
              <p>
                By using our service, you agree to our <a href="">Terms of Service</a>
                and <a href="">Privacy &amp; Cookie Statement</a>.
              </p>
              <v-btn
                color="primary"
                :disabled="invalid"
                v-on:click="onSubmit"
              >
                submit
              </v-btn>
            </v-container>
          </v-form>
        </v-container>
      </v-card>
    </div>
    <div>
      <v-carousel
        cycle
        hide-delimiters
        height="100vh"
        :show-arrows=false
        :interval="7000"
      >
        <v-carousel-item
          v-for="(slide,i) in slides"
          :key=i
          :src="slide.src"
          class="item"
          transition="fade-transition"
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
  </div>
</template>

<style>
.main-body {
  position: relative;
}
.v-carousel {
  height: calc(100vh - 48px) !important;
}
.v-window-item {
  position: absolute;
  top: 0;
  width: 100%;
}
.tag {
  height: calc(100vh - 48px);
  width: 100%;
}
.form-card {
  position: absolute;
  z-index: 1;
  top: 15%;
  left: 5%
}
</style>

<script>
export default {
  methods: {
    onSubmit () {
      let formData = new FormData();
      // this.files.forEach((file) => {
      //   formData.append(file);
      // });
      console.log(this.files);
    },
    onAdd () {
      this.files = this.newFiles.concat(this.files);
    },
    onClear () {
      this.files = [];
      this.newFiles = [];
    }
  },
  data () {
    return {
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
      ],
      valid: false,
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
      files: [],
      newFiles: []
    }
  }
}
</script>
