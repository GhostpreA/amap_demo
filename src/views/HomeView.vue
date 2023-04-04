<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <map-container></map-container>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import MapContainer from '@/map/MapContainer.vue'



export default {
  name: 'HomeView',
  components: {
    MapContainer,
    HelloWorld
  },

}
</script>
