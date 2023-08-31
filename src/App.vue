<template>
  <div id="app">
    <CenaComponent />
  </div>
</template>

<script>
import CenaComponent from './CenaComponent.vue'

export default {
  name: 'App',
  components: {
    CenaComponent
  }
}
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f0f0;
}
</style>
