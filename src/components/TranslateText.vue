<script setup>
import { Predictions } from 'aws-amplify'
import { ref, watch } from 'vue'

const inputText = ref('')
const translatedText = ref('翻訳する文字列')

const translate = (text) => {
  if (!text.length) {
    translatedText.value = ''
    return
  }

  // Text Translate の実装 ↓
  Predictions.convert({
  translateText: {
    source: {
      text: text,
    },
  },
})
  .then((result) => {
    translatedText.value = result.text;
  })
  .catch((error) => {
    console.warn({ error });
  });
  // ↑↑↑↑↑↑
}

watch(inputText, (inputText) => {
  translate(inputText)
})
</script>

<template>
  <v-container fluid="true" class="pa-0">
    <v-row class="ma-0 pa-0">
      <v-col cols="6" class="pa-0">
        <v-textarea v-model="inputText" placeholder="Type to translate." rows="20" />
      </v-col>
      <v-col cols="6" class="pa-0">
        <v-textarea v-model="translatedText" disabled rows="20" />
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>
v-textarea {
  font-size: 24px;
  border: none;
  outline: none;
  resize: none;
}
</style>
