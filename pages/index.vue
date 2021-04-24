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
        <v-stepper-step :complete="e1 > 3" step="3">
          Uploading
        </v-stepper-step>
        <v-divider></v-divider>
        <v-stepper-step :complete="e1 > 4" step="4">
          Summary
        </v-stepper-step>
      </v-stepper-header>
      <v-stepper-items>
        <validation-observer ref="observer" v-slot="{ invalid }">
          <v-form v-on:submit.prevent="onSubmit">
            <v-stepper-content step="1">
                <validation-provider v-slot="{ errors }" name="E-mail" rules="required|email">
                  <v-text-field v-model="email" :error-messages="errors" label="E-mail" required outlined class="pt-1"></v-text-field>
                </validation-provider>
              <v-btn color="primary" class="mr-2" @click="e1 = 2" :disabled="invalid">
                Continue
              </v-btn>
            </v-stepper-content>
            <v-stepper-content step="2">
              <v-data-table :headers="headers" :items="folders" sort-by="folder">
                <template v-slot:top>
                  <v-toolbar flat outlined>
                    <v-toolbar-title>
                      Selected folder(s)
                    </v-toolbar-title>
                    <v-divider class="mx-4" inset vertical></v-divider>
                    <v-spacer></v-spacer>
                      <input type="file" ref="uploadBox" style="display: none" multiple webkitdirectory v-on:change="onChange">
                      <v-btn @click="onAdd" class="mr-2" :loading="isSelectingFolders" color="success">Add folder</v-btn>
                      <v-btn @click="onClear" color="error">Clear</v-btn>
                  </v-toolbar>
                </template>
                <template v-slot:[`item.action`]="{ item }">
                  <v-icon small @click="onDelete(item.folder)" color="red">
                    mdi-delete
                  </v-icon>
                </template>
              </v-data-table>
              <v-btn color="primary" class="mr-2" @click="e1 = 1">
                Back
              </v-btn>
              <v-btn color="success" @click="e1 = 3" :disabled="invalid || !files.length" type="submit">
                Submit
              </v-btn>
            </v-stepper-content>
          </v-form>
        </validation-observer>
        <v-stepper-content step="3">
          <v-progress-linear v-model="progress" height="25">
            <strong>{{ progress }} %</strong>
          </v-progress-linear>
        </v-stepper-content>
        <v-stepper-content step="4">
          <strong>{{ folders.length }} folders</strong> have uploaded.<br>
          Check your inbox. Soon you will recieve an email from us.<br>
          Thank you for using our service.
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
  message: 'E-mail must be valid',
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
      const selectedFiles = [...e.target.files];
      this.folders.push({
        folder: selectedFiles[0].webkitRelativePath.split('/')[0]
      });
      this.files = this.files.concat(selectedFiles);
      e.target.value = '';
    },
    onClear () {
      this.files = [];
      this.folders = [];
    },
    onDelete (folderName) {
      this.folders.splice(this.folders.findIndex(e => e.folder === folderName));
      this.files = this.files.filter(e => e.webkitRelativePath.split('/')[0] !== folderName);
    }
  },
  data () {
    return {
      headers: [
        {
          text: 'Folder',
          aligb: 'start',
          sortable: true,
          value: 'folder'
        },
        { text: 'Action', value: 'action', sortable: false }
      ],
      e1: 1,
      valid: false,
      email: '',
      files: [],
      folders: [],
      progress: 0,
      isSelectingFolders: false,
    }
  }
}
</script>
