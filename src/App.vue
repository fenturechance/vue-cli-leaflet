<template>
  <div id="app">
    <LMap :zoom="zoom" :center="center" ref="mapObj">
      <LTileLayer :url="url" :attribution="attribution"></LTileLayer>
      <LMarker :lat-lng="marker"></LMarker>
      <LFeatureGroup ref="drawLayer">
        <leafletDraw :options="drawOption" :map-obj="mapObj"></leafletDraw>
      </LFeatureGroup>
    </LMap>
  </div>
</template>

<script>
import  { LMap, LTileLayer, LMarker , LFeatureGroup , LPopup } from 'vue2-leaflet';
import 'leaflet/dist/leaflet.css';
import leafletDraw from './components/leafletDraw';

export default {
  components: {
    LMap, LTileLayer, LMarker,
    LFeatureGroup,leafletDraw
  },
  data () {
    return {
      zoom:0,
      center: L.latLng(47.413220, -1.219482),
      url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution:'',
      marker: L.latLng(47.413220, -1.219482),
      drawOption: {
        position: 'topright',
        draw: {
            polyline:false,
            polygon: {
                allowIntersection: false, // Restricts shapes to simple polygons
                drawError: {
                    color: '#e1e100', // Color the shape will turn when intersects
                    message: '<strong>Oh snap!<strong> you can\'t draw that!' // Message that will show when intersect
                },
                shapeOptions: {
                    color: '#bada55'
                }
            },
            circle: false, // Turns off this drawing tool
            rectangle: false,
            marker: false,
            circlemarker : false
        },
        edit: {
            featureGroup : {},
            edit: {
                moveMarkers: false // centroids, default: false
            }
        }
      },
      mapObj: {}
    }
  },
  created() {
  },
  mounted() {
      this.mapObj = this.$refs.mapObj.mapObject;
      this.$nextTick(()=>{
        this.drawOption.edit.featureGroup = this.$refs.drawLayer.mapObject;
      })
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
