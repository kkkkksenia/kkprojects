<template>
  <div id="app">
    <main-component/>
  </div>
</template>

<script>
import mainComponent from './components/mainComponent'

export default {
  name: 'App',
  components: {
    'main-component': mainComponent
  }
}
</script>
