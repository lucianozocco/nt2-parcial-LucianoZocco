<template>
  <div id="app" class="container-fluid mt-3">
    <div class="jumbotron">
      <h1>Parcial PNT2 - 8-11-2022</h1>
      <br>
      <Navbar />
      <router-view></router-view>

    </div>
  </div>
</template>

<script>

import Navbar from './components/Navbar.vue'
export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
#app {
}

h1 {
  color: blue;
}
</style>
