<template>
  
</template>
<script>
    import 'leaflet-draw';
    import 'leaflet-toolbar';
    import 'leaflet-draw-toolbar/dist/leaflet.draw-toolbar.js';

    import 'leaflet-toolbar/dist/leaflet.toolbar.css';
    import 'leaflet-draw/dist/leaflet.draw.css';
    import 'leaflet-draw-toolbar/dist/leaflet.draw-toolbar.css';

    export default {
        props: ['options','mapObj'],
        mounted() {
            this.$nextTick(()=>{
                var drawnItems = this.options.edit.featureGroup.addTo(this.mapObj);
                new L.Toolbar2.DrawToolbar({ position: 'topleft' }).addTo(this.mapObj);
                this.mapObj.on('draw:created', (evt)=> {
                    var	type = evt.layerType,
                        layer = evt.layer;

                    drawnItems.addLayer(layer);

                    layer.on('click', (event)=> {
                        new L.Toolbar2.EditToolbar.Popup(event.latlng, {
                            actions: [
                                L.Toolbar2.EditAction.Popup.Edit,
                                L.Toolbar2.EditAction.Popup.Delete,
                            ]
                        }).addTo(this.mapObj, layer);
                    });
                });
            })
        },
    }
</script>
<style>

</style>

