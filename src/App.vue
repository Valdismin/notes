<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <div id="app">
        <main-component/>
      </div>
    </div>
  </div>
</template>

<script>
import MainComponent from './components/MainComponent.vue'

export default {
  name: 'App',
  components: {
    MainComponent
  }
}
</script>

<style>

</style>
