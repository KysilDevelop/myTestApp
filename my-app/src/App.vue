<template>
  <div id="app">
      <router-view></router-view>
  </div>
</template>

<script>
  //import your components here
  export default {
    name: 'app'
  }
</script>


Add "scoped" attribute to limit CSS to this component only
<style lang="scss">
  @import '../styles/normalize.scss';
  @import '../styles/style.scss';
</style>
