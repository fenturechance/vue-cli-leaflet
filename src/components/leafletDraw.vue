<template>
  
</template>
<script>
    import 'leaflet-draw';
    import 'leaflet-draw/dist/leaflet.draw.css';
    export default {
        props: ['options','mapObj'],
        mounted() {
            this.$nextTick(()=>{
                var drawControl = new L.Control.Draw(this.options);
                this.mapObj.addControl(drawControl);
                this.mapObj.on(L.Draw.Event.CREATED,(e)=> {
                    var type = e.layerType,
                        layer = e.layer;
                    if (type === 'marker') {
                        layer.bindPopup('A popup!');
                    }
                    this.options.edit.featureGroup.addLayer(layer);
                });
            })
        },
    }
</script>
