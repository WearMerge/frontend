<template>
  <div
    class="main-body"
  >
    <div
      class="form-card"
    >
      <v-card>
        <v-container
          v-if="progress === 0"
        >
          <v-row
            no-gutters
          >
            <v-col>
              <h1>
                Welcome!
              </h1>
            </v-col>
            <v-col>
              <div
                align="end"
              >
                <v-dialog
                  v-model="dialog"
                  width="500"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      icon
                      v-bind="attrs"
                      v-on="on"
                    >
                    <v-tooltip
                      bottom
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-icon
                          v-bind="attrs"
                          v-on="on"
                        >
                          mdi-information-outline 
                        </v-icon>
                      </template>
                      <span>Instructions</span>
                    </v-tooltip>
                    </v-btn>
                  </template> 
                  <v-card>
                    <v-card-title class="headline grey lighten-2">
                      Instructions
                    </v-card-title>
                    <v-card-text>
                      Something
                    </v-card-text>
                    <v-divider></v-divider>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn
                        color="primary"
                        text
                        @click="dialog = false"
                      >
                      close
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </div>
            </v-col>
          </v-row>
          <p>
            Please fill the following fields.
          </p>
          <validation-observer
            ref="observer"
            v-slot="{ invalid }"
          >
            <v-form
              v-on:submit.prevent="onSubmit"
            >
              <validation-provider
                v-slot="{ errors }"
                name="E-mail"
                rules="required|email"
              >
                <v-text-field
                  v-model="email"
                  :error-messages="errors"
                  label="E-mail"
                  required
                  outlined
                >
                </v-text-field>
              </validation-provider>
              <template>
                <div
                  v-if="!files.length"
                >
                <validation-provider
                  v-slot="{ errors }"
                  name="Add Folder"
                  rules="required|upload"
                >
                    <v-file-input
                      v-model="newFiles"
                      outlined
                      multiple
                      name="upload"
                      prepend-icon=""
                      label="Add Folder"
                      placeholder="Select a folder"
                      webkitdirectory
                      v-on:change="onAdd"
                      :error-messages="errors"
                    >
                    </v-file-input>
                </validation-provider>
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
                          <validation-provider
                            v-slot="{ errors }"
                            name="Add Folder"
                            rules="required|upload"
                          >
                            <v-file-input
                              v-model="newFiles"
                              multiple
                              hide-input
                              name="upload"
                              prepend-icon="mdi-paperclip"
                              webkitdirectory
                              v-on:change="onAdd"
                              v-on:click:clear="onClear"
                              v-on:mouseenter.native="on.mouseenter"
                              v-on:mouseleave.native="on.mouseleave"
                              :error-messages="errors"
                            >
                            </v-file-input>
                          </validation-provider>
                        </template>
                        <span>Add Folder</span>
                      </v-tooltip>
                    </div>
                    <v-btn
                      icon
                      v-on:click="onClear"
                    >
                      <v-tooltip
                          bottom
                        >
                          <template v-slot:activator="{ on, attrs }">
                            <v-icon
                              v-bind="attrs"
                              v-on="on"
                            >
                              mdi-window-close
                            </v-icon>
                          </template>
                        <span>Clear</span>
                      </v-tooltip>
                    </v-btn>
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
                type="submit"
              >
                submit
              </v-btn>
            </v-form>
          </validation-observer>
        </v-container>
        <v-container
          v-else-if="progress < 100 && progress > 0"
        >
          <h1>Upload progress</h1>
          <p>Please wait while your files are uploading.</p>
          <v-progress-linear
            v-model="progress"
            height="25"
          >
            <strong>
              {{ progress }} %
            </strong>
          </v-progress-linear>
        </v-container>
        <v-container
          v-else
        >
        <h1>Success</h1>
        <p>
          You just received an email from us!<br>
          Thank you for using our service.
        </p>
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
            align="end"
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
  left: 5%;
  width: 100%;
  max-width: 500px;
}
</style>

<script>
import { required, email } from 'vee-validate/dist/rules'
import { extend, ValidationObserver, ValidationProvider, setInteractionMode, Validator } from 'vee-validate'

setInteractionMode('eager')

extend('required', {
  ...required,
  message: '{_field_} cannot be empty',
})

extend('email', {
  ...email,
  message: 'Email must be valid',
})

extend('upload', {
  getMessage: field => field + 'cannot be empty',
  validate: value => this.files.length
})

export default {
  components: {
    ValidationProvider,
    ValidationObserver,
  },
  methods: {
    async onSubmit () {
      let formData = new FormData();
      formData.append('email', this.email);
      this.files.forEach((file) => {
       formData.append(file.webkitRelativePath.replace('/' + file.name, ''), file);
      });
      await this.$axios.$post('upload-file', formData, {
        onUploadProgress: (progressEvent) => {
          this.progress = Math.round((progressEvent.loaded * 100) / progressEvent.total);
        }
      });
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
      files: [],
      newFiles: [],
      progress: 0,
      dialog: false
    }
  }
}
</script>
