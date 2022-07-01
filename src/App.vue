<template>
  <div id="app">
    <main>
      <div class="weather-search">
        <input type="text" class="search__input" placeholder="Введите название города" v-model="country" />
        <button class="search__btn" @click="fetchWeather">
          SEARCH
        </button>
      </div>
      <div class="weather-main" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
            {{ weather.name }}
        </div>
        <div class="weather-temp">
          {{ Math.round(weather.main.temp) }}°C
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      api_key: "7f40938131da6e5fe5ebeaea4fe2d0da",
      url_base: "https://api.openweathermap.org/data/2.5/",
      country: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather() {
      fetch(
        `${this.url_base}weather?q=${this.country}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);

    },
    setResults(results) {
      this.weather = results;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

main {
  font-family: 'Roboto', sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
}

#app {
  background-image: url(./assets/warm-bg.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.weather-search {
  display: flex;
  justify-content: center;
  padding-top: 20px;
  margin-bottom: 200px;
}

.search__input {
  font-family: 'Roboto', sans-serif;
  font-size: 14px;
  width: 200px;
  height: 30px;
  outline: none;
  margin-right: 8px;
  padding: 5px;
  background-color: transparent;
  border: none;
  box-shadow: 0px 1px 8px rgba(0, 0, 0, 50%);
  border-radius: 5px 0px 5px 0px;
}

.search__btn {
  font-family: 'Roboto', sans-serif;
  font-size: 12px;
  width: 60px;
  background-color: #f8a81f;
  border: none;
  border-radius: 5px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 50%);
}
.search__btn:active {
  background-color: #d38e17;
}

.weather-main {
  background-color: rgba(255, 255, 255, 15%);
  padding: 50px;
  border-radius: 15px;
  box-shadow: 0px 4px 16px rgba(0, 0, 0, 55%);
}

.location-box {
  font-size: 23px;
  color: #fff;
  font-weight: 500;
  text-align: center;
}

.weather-temp {
  font-size: 50px;
  font-weight: 700;
  color: #fff; 
}
</style>