<script setup>
import { Predictions } from 'aws-amplify'
import { ref } from 'vue'

const uploadedImage = ref(null)
const response = ref('')

const identifyFromFile = (e) => {
  const file = e.target.files || e.dataTranfer.files
  if (!file) return

  createImage(file[0])

  //Identify Labels の実装
  Predictions.identify({
    labels: {
      source: {
        file: file[0]
      },
      type: 'LABELS'
    }
  })
    .then((result) => {
      response.value = result.labels
    })
    .catch((error) => console.warn(error))
  // ↑↑↑↑↑↑
}

const createImage = (file) => {
  const reader = new FileReader()
  reader.onload = (e) => {
    uploadedImage.value = e.target.result
  }
  reader.readAsDataURL(file)
}
</script>

<template>
  <v-file-input
    label="File input"
    variant="filled"
    prepend-icon="mdi-camera"
    accept="image/jpeg, image/png"
    @change="identifyFromFile"
  ></v-file-input>

  <v-container fluid="true" class="pa-0">
    <v-row class="ma-0 pa-0">
      <v-col cols="6" class="pa-0">
        <v-img :width="width" v-if="uploadedImage" :src="uploadedImage" />
      </v-col>
      <v-col cols="6" class="pa-0">
        <v-table>
          <thead>
            <tr>
              <th class="text-left">Name</th>
              <th class="text-left">Confidene</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in response" :key="item.name">
              <td>{{ item.name }}</td>
              <td>{{ item.metadata.confidence }}</td>
            </tr>
          </tbody>
        </v-table>
      </v-col>
    </v-row>
  </v-container>
</template>

