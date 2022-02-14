<template>
  <section class="api-container">
    <h1 tabindex="0">{{ msg }}</h1>
    <p class="overline italic" tabindex="0">like searching for gifs</p>
    <!-- use v-model directive for two-way data binding -->
    <input type="text" @keyup.enter="searchGifs" v-model.trim="userInput" placeholder="e.g. taylor swift">
    <!-- prevent modifier prevents default submission behaivor -->
    <button @click.prevent="searchGifs" type="button">Search</button>
    <!-- error messaging -->
    <div v-if="inputError || apiErrorMsg" class="error-messages">
      <p v-if="inputError" class="red uppercase" tabindex="0">{{inputErrorMsg}}</p>
      <p v-if="apiErrorMsg" class="red uppercase" tabindex="0">{{apiErrorMsg}}</p>
    </div>
    <!-- gif container -->
    <div class="gif-container">
      <!-- gif cards displayed using v-for directive -->
      <div class="gif-card" v-for="gif in gifs" :key="gif.id" tabindex="0">
        <img 
          :src="gif.images.fixed_width.url" 
          :alt="gif.title"
        />
        <div class="overlay">
          <a :href="gif.bitly_gif_url" target="_blank" aria-role="button" tabindex="0"><svg 
            xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M172.5 131.1C228.1 75.51 320.5 75.51 376.1 131.1C426.1 181.1 433.5 260.8 392.4 318.3L391.3 319.9C381 334.2 361 337.6 346.7 327.3C332.3 317 328.9 297 339.2 282.7L340.3 281.1C363.2 249 359.6 205.1 331.7 177.2C300.3 145.8 249.2 145.8 217.7 177.2L105.5 289.5C73.99 320.1 73.99 372 105.5 403.5C133.3 431.4 177.3 435 209.3 412.1L210.9 410.1C225.3 400.7 245.3 404 255.5 418.4C265.8 432.8 262.5 452.8 248.1 463.1L246.5 464.2C188.1 505.3 110.2 498.7 60.21 448.8C3.741 392.3 3.741 300.7 60.21 244.3L172.5 131.1zM467.5 380C411 436.5 319.5 436.5 263 380C213 330 206.5 251.2 247.6 193.7L248.7 192.1C258.1 177.8 278.1 174.4 293.3 184.7C307.7 194.1 311.1 214.1 300.8 229.3L299.7 230.9C276.8 262.1 280.4 306.9 308.3 334.8C339.7 366.2 390.8 366.2 422.3 334.8L534.5 222.5C566 191 566 139.1 534.5 108.5C506.7 80.63 462.7 76.99 430.7 99.9L429.1 101C414.7 111.3 394.7 107.1 384.5 93.58C374.2 79.2 377.5 59.21 391.9 48.94L393.5 47.82C451 6.731 529.8 13.25 579.8 63.24C636.3 119.7 636.3 211.3 579.8 267.7L467.5 380z"/>
          </svg></a> 
        </div>
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
                this.apiErrorMsg = "Nothing Found, Please enter your search in the box above";
              } 
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
            this.apiErrorMsg = null; // reset error msg after
            this.inputError = null;  // searching for new item
          }
      }
    }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "../scss/_variables.scss";
  @import "../scss/_typography.scss";
  @import "../scss/_buttons.scss";

  .api-container {
    padding-top: 5%;
    flex: 1 0 auto;

    h1 {
      margin: 10px;
      @media (min-width: $desktop) {
        margin: 0;
      }
    }

    .overline {
      margin-bottom: 32px;
    }

    input[type="text"] {
      font-family: $primary-font;
      letter-spacing: 0.5px;
      padding: 11px 10px 9px;
      border: 1px solid $red;
      width: 50%;
      line-height: 1rem;

      @media (min-width: $tablet) {
        width: 40%;
        padding: 11px 43px 9px 10px;
      }
    }

    .gif-container {
      column-count: 2;
      margin: 40px auto;
      padding: 0 8px;
      @media (min-width: $tablet){ 
        column-count: 3;
        max-width: 650px;
        padding: 20px;
      }
      @media (min-width: $desktop) {
        column-count: 3;
        max-width: 1000px;
      }

      .gif-card {
        display: grid;
        grid-template-rows: 1fr auto;
        break-inside: avoid; /* IE 10+ */
        -webkit-column-break-inside: avoid; /* Chrome, Safari, Opera */
        page-break-inside: avoid; /* Firefox */
        padding: 10px;
        position: relative;
        
        @media (min-width: $desktop) {
          gap: 0px;
          padding: 15px;
          &:not(:hover, :focus, :active, :focus-visible, :focus-within) {
            .overlay {
              visibility: hidden;
            }
          }     
        }

        img {
          width: 100%;
          display: block;
          @media (min-width: $tablet) {
            border-radius: 7px;
          }
        }

        .overlay {
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 10%;
          z-index: 2;
          text-align: left;

          svg {
            fill: $cream;
            width: 20px;
            height: 20px;
            background: $red;
            border-radius: 50%;
            padding: 5px;
            @media (min-width: $tablet) {
              margin: 20px 15px 0;
            }

            &:hover {
              background: $purple;
            }
          }
        }

        &:hover, &:focus {
          @media (min-width: $desktop) {
            img {
              transition: 0.15s all;
              -webkit-transition: 0.3s all;
              box-shadow: 2px 2px 7px 0px rgba($purple, 0.4);
              -webkit-box-shadow: 2px 2px 7px 0px rgba($purple, 0.4);
              transform: scale(1.1);
              border-radius: 7px;
            }
          }
        }
      }
    }
  }
</style>
