<template>
  
</template>
<script>
    import 'leaflet-draw';
    import 'leaflet-toolbar';

    import 'leaflet-toolbar/dist/leaflet.toolbar.css';
    import 'leaflet-draw/dist/leaflet.draw.css';

    export default {
        props: ['options','mapObj'],
        mounted() {
            this.$nextTick(()=>{
                var drawnItems = this.options.edit.featureGroup;
                this.mapObj.addLayer(drawnItems);
                var drawControl = new L.Control.Draw({
                    edit: {
                        featureGroup: drawnItems
                    }
                });
                this.mapObj.addControl(drawControl);
                this.mapObj.on(L.Draw.Event.CREATED, (evt)=> {
                    var	type = evt.layerType,
                        layer = evt.layer;

                    drawnItems.addLayer(layer);
                });
            })
        },
    }
</script>
<style>

</style>

