<script setup>
import { Predictions } from 'aws-amplify'
import { ref } from 'vue'

const uploadedImage = ref(null)
const words = ref([])

const identifyFromFile = (e) => {
  const file = e.target.files || e.dataTranfer.files
  if (!file) return

  createImage(file[0])

  // Identify Text の実装
  Predictions.identify({
    text: {
      source: {
        file: file[0]
      }
    }
  })
    .then((result) => {
      words.value = result.text.words
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

const getBoxStyles = (box) => {
  return {
    left: `${box.left * 100}%`,
    top: `${box.top * 100}%`,
    width: `${box.width * 100}%`,
    height: `${box.height * 100}%`,
    border: '2px solid red',
    position: 'absolute'
  }
}
</script>

<template>
  <v-file-input
    label="File input"
    variant="filled"
    prepend-icon="mdi-camera"
    @change="identifyFromFile"
    accept="image/jpeg, image/png"
  />
  <v-container fluid="true" class="pa-0">
    <v-row justify="center" class="ma-0 pa-0">
      <v-col cols="6" class="pa-0 position-relative">
        <v-img :width="width" v-if="uploadedImage" :src="uploadedImage" />
        <div v-if="words && words.length" class="bounding-box-container position-absolute">
          <div
            v-for="(word, index) in words"
            :key="index"
            class="bounding-box"
            :style="getBoxStyles(word.boundingBox)"
          ></div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>
.position-relative {
  position: relative;
}
.position-absolute {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.bounding-box {
  position: absolute;
}
</style>
