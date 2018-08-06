<template>
  <div id="app">
    <BaseMillions/>
  </div>
</template>

<script>
import BaseMillions from './components/BaseMillions.vue'

export default {
  name: 'app',
  components: {
    BaseMillions
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
