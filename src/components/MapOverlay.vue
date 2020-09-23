<template>
  <div class="map-container">
    <div class="info">
      <h1>Vue 2.x IP Address Tracker</h1>
    </div>
    <l-map
      :zoom="zoom"
      :center="center"
      @update:zoom="zoomUpdated"
      @update:center="centerUpdated"
      @update:bounds="boundsUpdated"
    >
      <l-marker
        :lat-lng="markerCoordinates"
        :icon="markerIcon" ></l-marker>
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    </l-map>
  </div>
</template>

<script>
import { LMap, LMarker, LTileLayer } from 'vue2-leaflet';
import { icon } from 'leaflet';
import LocationIcon from '../assets/icon-location.svg';
import 'leaflet/dist/leaflet.css';

export default {
  components: {
    LMap,
    LMarker,
    LTileLayer,
  },
  data() {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution: `&copy; OpenStreetMap ${new Date().getFullYear()}`,
      zoom: 6,
      center: [31.623812, 34.541016],
      markerCoordinates: [31.997113, 34.782715],
      markerIcon: icon({
        iconUrl: LocationIcon,
        iconSize: [28, 35],
        iconAnchor: [16, 37],
      }),
      bounds: null,
    };
  },
  methods: {
    zoomUpdated(zoom) {
      this.zoom = zoom;
    },
    centerUpdated(center) {
      this.center = center;
    },
    boundsUpdated(bounds) {
      this.bounds = bounds;
    },
  },
};
</script>

<style lang="scss">
.map-container {
  height: 85vh;

  .info {
    height: 15vh;

    h1 {
      margin-top: 0;
      padding-top: 20px;
      color: white;
    }
  }
}
</style>
