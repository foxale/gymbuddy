<template>
  <div class="app">
    <NavigationBar />
    <CityMap />
  </div>
</template>

<script>
import NavigationBar from './components/NavigationBar.vue';
import CityMap from './components/CityMap.vue';

export default {
  name: 'App',
  components: {
    NavigationBar,
    CityMap
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}

.app {
  text-align: center;
}
</style>
