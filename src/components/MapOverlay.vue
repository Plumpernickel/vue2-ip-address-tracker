<template>
  <div class="map-container">
    <div class="info">
      <h1>
        <img class="title-logo" src="../assets/logo.png" alt="Vue logo" />
        <span>{{' '}}IP Address Tracker</span>
      </h1>
      <IpForm v-on:update:latlng="handleUpdateLatLng" />
    </div>
    <l-map
      class="map-content"
      :zoom="zoom"
      :center="center"
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
import IpForm from './IpForm.vue';
import LocationIcon from '../assets/icon-location.svg';
import 'leaflet/dist/leaflet.css';

export default {
  components: {
    IpForm,
    LMap,
    LMarker,
    LTileLayer,
  },
  data() {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution: `&copy; OpenStreetMap ${new Date().getFullYear()}`,
      zoom: 13,
      center: [31.997113, 34.782715],
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
    handleUpdateLatLng($event) {
      if ($event[0] && $event[1]) {
        this.center = $event;
        this.markerCoordinates = $event;
      }
    },
  },
};
</script>

<style lang="scss">
.map-container {
  height: 75vh;

  .info {
    height: 15vh;

    h1 {
      margin-top: 0;
      color: white;
      font-weight: 500;

      .title-logo {
        width: 64px;
        vertical-align: middle;
      }
    }
  }

  .map-content {
    margin-top: calc(225px - 15vh);
  }
}
</style>
