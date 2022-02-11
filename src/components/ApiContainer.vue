<template>
  <div class="api-container">
    <h1>{{ msg }}</h1>
    <!-- use v-model directive for two-way data binding -->
    <input type="text" v-model="userInput">
    <button @click="searchGifs">Go</button>
  </div>
</template>

<script>
  // import axios from "axios";

  export default {
    name: 'ApiContainer',
    props: {
      msg: String
    },
    //function called data that returns an object
    data(){
      return {
        userInput: 'hello'
      };
    },
    methods: {
      searchGifs() {
        console.log('searchin for gifs');
        console.log(this.userInput);
      }
    }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
