<template>
  <div id="app">
    <VueNavbar />
    <VueArtigos />
  </div>
</template>

<script>

import VueArtigos from './components/Artigos.vue'
import VueNavbar from './components/Navbar.vue'


export default {
  name: 'App',
  components: {
    VueArtigos,
    VueNavbar
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-decoration: none;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
