<template>
  <ApiContainer msg="I don't know about you, but I'm feeling"/>
  <Footer />
</template>

<script>
import ApiContainer from './components/ApiContainer.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    ApiContainer,
    Footer
  }
}
</script>

<!-- not scoped -->
<style lang="scss">
  @import "./scss/_variables.scss";
  @import "./scss/_typography.scss";
// initial css from vue 3 template
  #app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  html {
    background-color: $cream;
  }

  html, body {
    height: 100%;
    margin: 0;
    padding: 0;
  }

</style>
