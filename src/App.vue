<template>
  <div id="app">
    <VueNavbar />
    <VueArtigos />
    <VueFooter />
  </div>
</template>

<script>

import VueArtigos from './components/Artigos.vue'
import VueNavbar from './components/Navbar.vue'
import VueFooter from './components/Footer.vue'


export default {
  name: 'App',
  components: {
    VueArtigos,
    VueNavbar,
    VueFooter
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-decoration: none;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
