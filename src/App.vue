<template>
  <div id="app">
    <SongList/>
  </div>
</template>

<script>
import Vue from 'vue'
import VueMaterial from 'vue-material'
import VueResource from 'vue-resource'
import 'vue-material/dist/vue-material.min.css'

Vue.use(VueMaterial)
Vue.use(VueResource)
Vue.use(require('vue-moment'));

import SongList from './components/SongList.vue'

export default {
  name: 'app',
  components: {
    SongList
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
