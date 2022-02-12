<template>
  <div class="api-container">
    <h1>{{ msg }}</h1>
    <!-- use v-model directive for two-way data binding -->
    <input type="text" v-model.trim="userInput">
    <button @click="searchGifs" type="button">Go</button>
    <img v-for="gif in gifs" :key="gif.id" :src="gif.images.fixed_height_small.url" />
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    name: 'ApiContainer',
    props: {
      msg: String
    },
    //function called data that returns an object
    data(){
      return {
        userInput: 'hello',
        gifs: []
      };
    },
    methods: {
      searchGifs() {
        console.log(this.userInput, "this is user input")
        let APIkey = '2smyGBe8j335aBYmZqyRtcDIO6c0ff5B';
        let url = 'https://api.giphy.com/v1/gifs/search?api_key=' + APIkey + '&q=';
        let apiLink = url + this.userInput;

        axios
          .get(apiLink)
          .then((response) => {
            this.gifs = response.data.data;
          })
          .catch((error) => {
            console.log(error);
          })
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
