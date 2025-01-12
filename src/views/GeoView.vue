<script setup>
import { createMap, createAmplifyGeocoder } from 'maplibre-gl-js-amplify'
import { NavigationControl } from 'maplibre-gl'
import 'maplibre-gl/dist/maplibre-gl.css'
import '@maplibre/maplibre-gl-geocoder/dist/maplibre-gl-geocoder.css'

const mapCreate = async () => {
  const map = await createMap({
    container: 'map',
    center: [139.7157, 35.634],
    zoom: 10
  })

  const geocoder = createAmplifyGeocoder({
    flyTo: { maxZoom: 13 }
  })

  map.addControl(geocoder)
  map.addControl(new NavigationControl({ visualizePitch: true }))
}

mapCreate()
</script>

<template>
  <div id="map-container" class="map-container">
    <div id="map" class="map" />
  </div>
</template>

<style scoped>
.map-container {
  width: 100%;
  height: calc(100vh - 112px);
  align-items: center;
  justify-content: center;
  position: relative;
}

.map {
  width: 100%;
  height: 100%;
}
</style>
