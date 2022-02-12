<template>
  <ApiContainer msg="I don't know about you, but I'm feeling"/>
</template>

<script>
import ApiContainer from './components/ApiContainer.vue'

export default {
  name: 'App',
  components: {
    ApiContainer
  }
}
</script>

<!-- not scoped -->
<style lang="scss">
  @import "./scss/_variables.scss";
  @import "./scss/_typography.scss";
// initial css from vue 3 template
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
  }

  html {
    background-color: $cream;
  }
</style>
