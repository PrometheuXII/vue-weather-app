<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search...">
      </div>

      <div class="main-container">
        <div class="location-container">
          <div class="location">Manila, Philippines</div>
          <div class="date">Wednesday, March 23 2022</div>
        </div>

        <div class="weather-container">
          <div class="temperature">9°c</div>
          <div class="status">Rain</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  setup(){
    return {
      api_key: '903ac2bba7987881cae5396c6d2df314'
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
