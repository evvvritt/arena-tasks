<template lang="pug">
  #app.font-sans
    home
</template>

<script>
import '@/style/_main.css'
import Home from '@/views/Home'
export default {
  name: 'app',
  components: { Home }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size:16px;
}
</style>
