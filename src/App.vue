<template>
  <div id="app">
    <router-view/>
    <mainTabbar/>
  </div>
</template>

<script>
  import mainTabbar from 'components/content/mainTabbar/maintabbar'

  export default {
    name: 'App',
    components: {
      mainTabbar,
    }
  }
</script>

<style>
  @import "assets/css/base.css";
</style>
