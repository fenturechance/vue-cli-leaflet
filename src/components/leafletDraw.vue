<template>
  
</template>
<script>
    import 'leaflet-draw';
    export default {
        props: ['options','mapObj'],
        mounted() {
            this.$nextTick(()=>{
                var drawControl = new L.Control.Draw(this.options);
                this.mapObj.addControl(drawControl);
            })
        }
    }
</script>