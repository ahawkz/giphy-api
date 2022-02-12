<template>
  <div class="api-container">
    <h1>{{ msg }}</h1>
    <p class="overline">like searching for gifs</p>
    <!-- use v-model directive for two-way data binding -->
    <input type="text" v-model.trim="userInput">
    <button @click="searchGifs" type="button">Search</button>
    <div class="gif-container">
      <div class="gif-card" v-for="gif in gifs" :key="gif.id">
        <img 
          :src="gif.images.fixed_height_small.url" 
          :alt="gif.title"
        />
        <p>Share {{gif.url}}</p>
      </div>

    </div>
  </div>
</template>

<script>
  import axios from "axios"; 
  //promise-based http client that works in the browser and node 

  export default {
    name: 'ApiContainer',
    props: {
      msg: String
    },
    //function called data that returns an object
    data(){
      return {
        userInput: 'taylor swift',
        gifs: []
      };
    },
    methods: {
      searchGifs() {
        let APIkey = '2smyGBe8j335aBYmZqyRtcDIO6c0ff5B';
        let url = 'https://api.giphy.com/v1/gifs/search?api_key=' + APIkey + '&limit=13&rating=pg-13&&lang=en&q=';
        let apiLink = url + this.userInput;

        axios
          .get(apiLink)
          .then((response) => {
            console.log(response.data.data);
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
<style scoped lang="scss">
  .api-container {
    margin-top: 100px;

    h1 {
    margin: 0;
    }

    .overline {
      text-transform: uppercase;
      margin-top: 0;
    }
  }
</style>
