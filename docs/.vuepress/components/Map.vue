<template>
  <div class="map-container">
    <div class="overlay" v-show="isOpen">
      <div class="times">
        Aperto da martedì a giovedì dalle 12 alle 19,30<br>
          venerdì dalle 9 alle 19<br>
          sabato dalle 9 alle 17<br>
        </div>
        <div class="place">
          Torre Lasie - via Lasie 10/L<br>
            40026 Imola (Bo)<br>
            +39 0542 643314<br>
            studiomparrucchieri@gmail.com
          <button v-on:click='isOpen = !isOpen'>Naviga la mappa</button>
        </div>
      </div>
      <button class="close" v-show="!isOpen" v-on:click='isOpen = !isOpen'>Chiudi</button>
      <l-map :options="{zoomControl: false, attributionControl: false}" :zoom="zoom" :center="center">
        <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
        <l-marker :lat-lng="marker"></l-marker>
      </l-map>
    </div>
</template>

<script>
  import { LMap, LTileLayer, LMarker } from 'vue2-leaflet';

  export default {
    name: 'Example',
    components: {
      LMap,
      LTileLayer,
      LMarker
    },
    data () {
      delete L.Icon.Default.prototype._getIconUrl  
      L.Icon.Default.mergeOptions({  
        iconRetinaUrl: require('../public/location-pin.svg'),
        iconUrl: require('../public/location-pin.svg'),
        shadowUrl: ''
      })

      return {
        isOpen: true,
        zoom: 15,
        center: L.latLng(44.3771006,11.7263129),
        url: 'https://cartodb-basemaps-{s}.global.ssl.fastly.net/dark_all/{z}/{x}/{y}{r}.png',
        attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
        currentZoom: 13,
        marker: L.latLng(44.3771006,11.7263129),
        currentCenter: L.latLng(44.3771006,11.7263129)
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
        background: fade_out(white, 0.5);

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        > * + * {
            margin-top: 2rem;
        }

        > * {
            color: black;
            padding: 1rem;
            position: relative;

            &:after {
                content: '';
                z-index: -1;
                position: absolute;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                background: white;

                transform: skewY(2deg);
            }
        }
    }

    .vue2leaflet-map {
        z-index: 1;
    }
}
</style>
