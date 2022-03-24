<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..."
          v-model="query"
          @keypress="getWeather"
        >
      </div>
      <!-- v-if="typeof weather.main != 'undefined'" -->
      <div class="main-container" v-if="typeof weather.main != 'undefined'" >
        <div class="location-container">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-container">
          <div class="temperature">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="status">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import { ref } from '@vue/reactivity'

export default {
  name: 'app',
  setup(){
    let query = ref('');
    let weather = ref([]);
    // const getWeather = async (e) => {
    //   if(e.key == "Enter"){
    //     await axios.get(
    //       'https://api.openweathermap.org/data/2.5/weather?q=Manila&units=metric&APPID=903ac2bba7987881cae5396c6d2df314'
    //     ).then(response => (weather = response.data))
    //     .catch((error) => {
    //       console.log(error);
    //     })
    //   }
    // }
    // watch(query, async(newQuery, oldQuery) => {
    //   if(newQuery.length > 0){

    //   }
    // })
    return {
      api_key: '903ac2bba7987881cae5396c6d2df314',
      url_base: "https://api.openweathermap.org/data/2.5/",
      query,
      weather,
    }
  },
  methods: {
    async getWeather(e) {
      if(e.key == "Enter"){
        await axios.get(this.url_base + "weather?q=" + this.query + "&units=metric&APPID="+ this.api_key)
        .then(res => (this.weather = res.data))
      }
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return day +', '+ date +' '+ month +' '+ year; 
    }
  }


}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'Poppins' ,sans-serif;
  }

  #app{
    background-image: url('./assets/cold-bg.jpg');
    background-size: cover;
    background-position: bottom;

    transition: 0.4s;
  }

  #app.warm {
    background-image: url('./assets/warm-bg.jpg');
  }

  main{
    min-height: 100vh;
    padding: 25px;

    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
  }

  .search-box{
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar{
    display: block;
    width: 100%;
    padding: 15px;

    color: #313131;
    font-size: 20px;
    
    appearance: none;
    border: none;
    outline: none;
    background: none;

    
    box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 400ms;
  }

  .search-box .search-bar:focus{
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.75);
    border-radius: 16px 0px 16px 0px;
  }

  .location-container{
    margin-bottom: 10px;
  }

  .location-container .location{
    color: #fff;
    font-size: calc(2vw + 1.2em);
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  }

  .location-container .date{
    color: #fff;
    font-size: calc(1vw + .75em);
    font-weight: 500;
    text-align: center;
    font-style: italic;
  }

  .weather-container{
    margin: 0 auto;
    min-width: 150px;
    max-width: 350px;
    width: auto;
    padding: 25px;

    border-radius: 15px;
    background-color: rgba(255, 255, 255, 0.75);
    text-align: center;
  }

  .weather-container .temperature{
    display: inline-block;
    color: #000;
    font-size: calc(3vw + 2.5em);
    font-weight: 900;
    
    text-shadow: 2px 2px rgba(0, 0, 0, .25);
  }

  .weather-container .status{
    color: #000;
    font-size: calc(1vw + .75em);
  }
</style>
