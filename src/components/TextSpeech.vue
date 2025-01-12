<script setup>
import { Predictions } from 'aws-amplify'
import { ref } from 'vue'

const inputText = ref('')
const rules = ref([
  (value) => {
    if (value) return true

    return 'You must enter a text.'
  }
])
const speech = (e) => {
  e.preventDefault()
  // Text Speech の実装
  Predictions.convert({
    textToSpeech: {
      source: {
        text: inputText.value
      }
    }
  })
    .then((result) => {
      const AudioContext = window.AudioContext || window.webkitAudioContext
      const audioCtx = new AudioContext()
      const source = audioCtx.createBufferSource()

      audioCtx.decodeAudioData(result.audioStream, (buffer) => {
        source.buffer = buffer
        source.connect(audioCtx.destination)
        source.start(0)
      })
    })
    .catch((error) => console.warn(error))

  // ↑↑↑↑↑↑
}
</script>

<template>
  <v-form @submit.prevent>
    <v-text-field v-model="inputText" :rules="rules" @click="speech"></v-text-field>
  </v-form>
</template>
