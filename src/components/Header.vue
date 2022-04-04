<template>
  <div>
    <h1 tabindex="0">{{ msg }}</h1>
    <p class="overline italic" tabindex="0">like searching for gifs</p>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  }
}
</script>

<style>
  @import "../scss/_variables.scss";
  @import "../scss/_typography.scss";
  @import "../scss/_buttons.scss";

  h1 {
    padding-top: 5%;
    flex: 1 0 auto;
    margin: 10px;
    @media (min-width: $desktop) {
      margin: 0;
    }
  }

  .overline {
    margin-bottom: 32px;
  }
</style>