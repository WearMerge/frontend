<template>
  <v-container>
    <v-stepper v-model="e1">
      <v-stepper-header>
        <v-stepper-step :complete="e1 > 1" step="1">
          Personal informations
        </v-stepper-step>
        <v-divider></v-divider>
        <v-stepper-step :complete="e1 > 2" step="2">
          Select your folders
        </v-stepper-step>
        <v-divider></v-divider>
        <v-stepper-step step="3">
          Summary
        </v-stepper-step>
      </v-stepper-header>
      <v-stepper-items>
        <v-stepper-content step="1">
          <validation-observer ref="observer" v-slot="{ invalid }">
            <validation-provider v-slot="{ errors }" name="E-mail" rules="required|email">
              <v-text-field v-model="email" :error-messages="errors" label="E-mail" required outlined>
              </v-text-field>
            </validation-provider>
          </validation-observer>
          <v-btn color="primary" @click="e1 = 2">
            Continue
          </v-btn>
        </v-stepper-content>
        <v-stepper-content step="2">
          <v-toolbar flat outlined>
            <v-toolbar-title>
              Selected folder(s)
            </v-toolbar-title>
            <v-divider class="mx-4" inset vertical></v-divider>
              <input type="file" ref="uploadBox" style="display: none" multiple webkitdirectory v-on:change="onChange">
              <v-btn @click="onAdd" :loading="isSelectingFolders">open file dialog</v-btn>
          </v-toolbar>
          <v-btn color="primary" @click="e1 = 1">
            Back
          </v-btn>
          <v-btn color="primary" @click="e1 = 3">
            Continue
          </v-btn>
        </v-stepper-content>
        <v-stepper-content step="3">
          <v-card class="md-12">
          </v-card>
          <v-btn color="primary" @click="e1 = 2">
            Back
          </v-btn>
          <v-btn color="primary" @click="e1 = 1">
            Continue
          </v-btn>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </v-container>
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
      this.isSelectingFolders = true;
      window.addEventListener('focus', () => {
        this.isSelectingFolders = false;
      }, { once: true });
      this.$refs.uploadBox.click();
    },
    onChange (e) {
      this.files = this.files.concat([...e.target.files]);
      console.log(this.files);
    },
    onClear () {
      this.files = [];
      this.newFiles = [];
    }
  },
  data () {
    return {
      e1: 1,
      valid: false,
      email: '',
      files: [],
      newFiles: [],
      progress: 0,
      dialog: false,
      isSelectingFolders: false,
    }
  }
}
</script>
