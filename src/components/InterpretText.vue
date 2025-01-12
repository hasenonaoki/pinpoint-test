<script setup>
import { Predictions } from 'aws-amplify'
import { ref } from 'vue'

const inputText = ref('')
const response = ref('')

const interpretation = (e) => {
  e.preventDefault()

  // Interpret Textの実装
  Predictions.interpret({
    text: {
      source: {
        text: inputText.value
      },
      type: 'ALL'
    }
  })
    .then((result) => {
      console.log(result.textInterpretation.textEntities)
      response.value = result.textInterpretation.textEntities
    })
    .catch((error) => console.warn(error))
  // ↑↑↑↑↑↑
}
</script>

<template>
  <v-container fluid="true" class="pa-0">
    <v-row class="ma-0 pa-0">
      <v-col cols="6" class="pa-0">
        <v-textarea
          class="ioarea"
          v-model="inputText"
          placeholder="Type to interpret.（Press Shift + Enter）"
          @keydown.enter.shift="interpretation"
          rows="20"
      /></v-col>
      <v-col cols="6" class="pa-0">
        <v-table>
          <thead>
            <tr>
              <th class="text-left">Text</th>
              <th class="text-left">Type</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in response" :key="item.text">
              <td>{{ item.text }}</td>
              <td>{{ item.type }}</td>
            </tr>
          </tbody>
        </v-table>
      </v-col>
    </v-row>
  </v-container>
</template>

