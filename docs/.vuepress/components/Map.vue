<template>
  <div class="map-container">
    <div class="overlay" v-show="isOpen">
      <button v-on:click='isOpen = !isOpen'>Mostra la mappa</button>
    </div>
    <button class="close" v-show="!isOpen" v-on:click='isOpen = !isOpen'>Chiudi</button>
    <div class="map-wrapper" id="map-wrapper"></div>
  </div>
</template>

<script>
  export default {
    name: 'Map',
    mounted() {
      const { LMap, LTileLayer, LMarker } = require('vue2-leaflet');
      const position = L.latLng(44.3771006,11.7263129);

      const map = L.map('map-wrapper', {
        zoomControl: false
      }).setView(position, 16);
      
      L.tileLayer('https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}{r}.png', {
        attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>'
      }).addTo(map);

      const icon = L.icon({
        iconUrl: '/location-pin.svg',
        iconSize: [38, 95],
        iconAnchor: [22, 94]
      });

      L.marker(position, {icon: icon}).addTo(map);
    },
    data () {
      return {
        isOpen: true,
      };
    }
  };
</script>

<style lang="scss" scoped>
@import '../../../node_modules/leaflet/dist/leaflet.css';

.map-container {
    width: 100%;
    height: 100%;
    position: relative;

    .close {
        position: absolute;
        top: 4rem;
        left: 2rem;
        margin: 0;
        z-index: 2;
    }

    button {
        margin: 1rem auto;
        display: block;
        background: black;
        color: white;
        padding: 1rem;
        font-size: 1.2rem;
        text-transform: uppercase;
        font-family: 'Oswald';
        font-weight: 200;
        outline: none;
        cursor: pointer;
        position: relative;
        &:before {
            content: '';
            position: absolute;
            left: 10%;
            bottom: 0.6rem;
            width: 80%;
            height: 2px;
            background: white;
            transform: scaleX(0);
            transition: transform 300ms ease;
        }

        &:hover {
            &:before {
                transform: scaleX(1);
            }
        }
    }

    .overlay {
        padding-top: 3rem;
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        z-index: 2;
        background: fade_out(black, 0.5);

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .map-wrapper {
        width: 100%;
        height: 100%;
        z-index: 1;
        overflow: hidden;
    }
}
</style>
