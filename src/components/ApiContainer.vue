<template>
  <section class="api-container">
    <h1 tabindex="0">{{ msg }}</h1>
    <p class="overline" tabindex="0">like searching for gifs</p>
    <!-- use v-model directive for two-way data binding -->
    <input type="text" v-model.trim="userInput" placeholder="taylor swift">
    <!-- prevent modifier prevents default submission behaivor -->
    <button @click.prevent="searchGifs" type="button">Search</button>

    <div class="error-messages">
      <p v-if="inputError" class="red uppercase" tabindex="0">{{inputErrorMsg}}</p>
      <p v-if="apiErrorMsg" class="red uppercase" tabindex="0">Error: {{apiErrorMsg}}</p>
    </div>

    <div class="gif-container">
      <!-- gif cards displayed using v-for directive -->
      <div class="gif-card" v-for="gif in gifs" :key="gif.id">
        <img 
          :src="gif.images.fixed_height_small.url" 
          :alt="gif.title"
        />
        <p>Share {{gif.url}}</p>
      </div>
    </div> 
  </section>
</template>

<script>
  import axios from "axios";  //promise-based http client that works in the browser and node 

  export default {
    name: 'ApiContainer',
    props: {
      msg: String
    },
    //function called data that returns an object
    data(){
      return {
        userInput: '',
        gifs: [],
        inputError: false,
        inputErrorMsg: '*Input Required',
        apiErrorMsg: ''
      };
    },
    methods: {
      searchGifs() {
        let APIkey = '2smyGBe8j335aBYmZqyRtcDIO6c0ff5B';
        let url = 'https://api.giphy.com/v1/gifs/search?api_key=' + APIkey + '&limit=13&rating=pg-13&&lang=en&q=';
        let apiLink = url + this.userInput;

        if(!this.userInput && this.userInput) {
          this.inputError = true;
        } else {
          this.inputError = false;
          axios
            .get(apiLink)
            .then((response) => {
              this.gifs = response.data.data;
              if (this.gifs < 1) {
                this.apiErrorMsg = "Nothing Found";
              }
              console.log("META", response.data.meta);
              console.log(response.data.data);
            })
            .catch((error) => {
              console.log("error", error);

              if(error.response) {
                // client received an error response 
                console.log("error response", error.response)
                this.apiErrorMsg = error.response.data.meta.msg;
              } else if (error.request) {
                // client never received a response
                // usually responds with a network error 
                console.log("error request", error.request)
                this.apiErrorMsg = "Network Error";
              } else {
                // error is likely not coming from axios
                console.log(error);
              }
            })
            this.userInput = '';
          }
      }
    }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "../scss/_variables.scss";
  @import "../scss/_typography.scss";

  .api-container {
    margin-top: 10%;

    h1 {
      margin: 10px;
      @media (min-width: $desktop) {
        margin: 0;
      }
    }

    input[type="text"] {
      font-family: $primary-font;
      letter-spacing: 0.5px;
      padding: 5px;
    }

    .gif-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      @media (min-width: $desktop) {
        padding: 100px;
      }

    }

    .gif-card {
      width: 100%;
      border: 1px solid green;
      border-radius: 10%;
      
      @media (min-width: $desktop) {
        width: 33%;
      }
    }
  }
</style>
