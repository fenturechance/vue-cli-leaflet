<template>
  
</template>
<script>
    import 'leaflet-draw';
    import 'leaflet-toolbar';
    import 'leaflet-draw-drag';
    import 'leaflet-draw-toolbar/dist/leaflet.draw-toolbar.js';

    import 'leaflet-toolbar/dist/leaflet.toolbar.css';
    import 'leaflet-draw/dist/leaflet.draw.css';
    import 'leaflet-draw-toolbar/dist/leaflet.draw-toolbar.css';

    export default {
        props: ['options','mapObj'],
        mounted() {
            this.$nextTick(()=>{
                var drawnItems = this.options.edit.featureGroup;
                this.mapObj.addLayer(drawnItems);
                var drawControl = new L.Control.Draw(this.options);
                this.mapObj.addControl(drawControl);
                this.mapObj.on(L.Draw.Event.DELETED, (evt)=> {
                    this.mapObj.addControl(drawControl);
                });
                this.mapObj.on(L.Draw.Event.CREATED, (evt)=> {

                    var	type = evt.layerType,
                        layer = evt.layer;
                    drawnItems.addLayer(layer);
                    this.mapObj.removeControl(drawControl);
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

