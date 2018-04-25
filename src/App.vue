<template>
  <div id="app">
    <LMap :zoom="zoom" :center="center">
      <LTileLayer :url="url" :attribution="attribution"></LTileLayer>
      <LMarker :lat-lng="marker"></LMarker>
      <v-protobuf :url="url" :options="options"></v-protobuf>
    </LMap>
  </div>
</template>

<script>
import  { LMap, LTileLayer, LMarker } from 'vue2-leaflet';
import 'leaflet/dist/leaflet.css';
import Vue2LeafletVectorGridProtobuf from 'vue2-leaflet-vectorgrid';

export default {
  components: {
    LMap, LTileLayer, LMarker,
    'v-protobuf': Vue2LeafletVectorGridProtobuf
  },
  data () {
    return {
      zoom:0,
      center: L.latLng(47.413220, -1.219482),
      url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution:'',
      marker: L.latLng(47.413220, -1.219482),
      options: {
        vectorTileLayerStyles:{
        },
      }
    }
  },
  mounted() {
  }
}
</script>

<style>
#app {
  overflow-x: auto;
  height: 500px;
  width: 100%
}

</style>