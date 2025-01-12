<script setup>
import TranslateText from '../components/TranslateText.vue'
import IdentifyLabels from '../components/IdentifyLabels.vue'
import IdentifyText from '../components/IdentifyText.vue'
import InterpretText from '../components/InterpretText.vue' 
import TextSpeech from '../components/TextSpeech.vue'
</script>

<template>
  <v-expansion-panels variant="accordion">
    <v-expansion-panel>
      <v-expansion-panel-title>Translate - Amazon Translate</v-expansion-panel-title>
      <v-expansion-panel-text>
        <!-- <TranslateText /> -->
        <TranslateText /> 
      </v-expansion-panel-text>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-title>Identify Labels - Amazon Rekognition </v-expansion-panel-title>
      <v-expansion-panel-text>
        <!-- <IdentifyLabels /> -->
        <IdentifyLabels /> 
      </v-expansion-panel-text>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-title>Identify Text - Amazon Rekognition</v-expansion-panel-title>
      <v-expansion-panel-text>
        <!-- <IdentifyText /> -->
	<IdentifyText />
      </v-expansion-panel-text>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-title>Interpret Text - Amazon Comprenhend</v-expansion-panel-title>
      <v-expansion-panel-text>
        <!-- <InterpretText /> -->
	<InterpretText />
      </v-expansion-panel-text>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-title>Text to Speech - Amazon Polly</v-expansion-panel-title>
      <v-expansion-panel-text>
        <!-- <TextSpeech /> -->
	<TextSpeech />
      </v-expansion-panel-text>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<style scoped>
:deep([class^='v-expansion-panel-text']) {
  padding: 0 !important;
}

:deep(.v-expansion-panel--active .v-expansion-panel-title) {
  background-color: #242c3c !important;
  color: white !important;
}
</style>

