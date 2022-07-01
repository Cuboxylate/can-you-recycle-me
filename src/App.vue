<template>
<div>
  <h2>Gomeco Vision</h2>
            
  <div id="camera">
    <CameraSnapVue @picture-taken="imgSrc = $event"/>
    <img :src="imgSrc" />
  </div>
</div>
</template>
 
<script>
    import CameraSnapVue from './components/CameraSnap.vue';
 
    export default {
        name: "Camera",
        components: {
            CameraSnapVue
        },
        data() {
          return {
            imgSrc: null
          }
        }
        
    }
</script>
 
<style scoped>
    .camera-box {
        border: 1px dashed #d6d6d6;
        border-radius: 4px;
        padding: 2px;
        width: 80%;
        min-height: 300px;
    }
 
</style>