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
            })
        },
    }
</script>
