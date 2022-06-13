<template>
  <PortfolioVue title="Image Gallery" />
</template>

<script>
import PortfolioVue from './components/portoflio/Portfolio.vue'

export default {
  name: 'App',
  components: {
    PortfolioVue
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
