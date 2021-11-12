<template>
  <div class="weather-title">
    <h1>Weather</h1>
    <input
      v-model="location"
      class="city-search"
      placeholder="Type the name of the city"
      type="text"
    />
    <button @click="updateLocation()">Search</button>
    <h2>Weather in {{ location }}</h2>
    <div class="weather__boxes">
      <div class="box">
        <h4>{{ getDate(0) }}</h4>
        <ul>
          <li
            class="list"
            v-for="weather in getDateWeather(0)"
            :key="weather.dt"
          >
            <p>
              {{ weather.dt_txt }}
            </p>
            <p>
              Weather: {{ weather.weather[0].main }} -
              {{ weather.weather[0].description }}
            </p>

            <img :src="getWeatherIcons(weather.weather[0].icon)" width="30%" />

            <span
              ><p class="temp">{{ parseInt(weather.main.temp) }}°C</p>
            </span>
          </li>
        </ul>
      </div>
      <div class="box">
        <h4>{{ getDate(1) }}</h4>

        <ul>
          <li
            class="list"
            v-for="weather in getDateWeather(1)"
            :key="weather.dt"
          >
            <p>
              {{ weather.dt_txt }}
            </p>
            <p>
              Weather: {{ weather.weather[0].main }} -
              {{ weather.weather[0].description }}
            </p>
            <img :src="getWeatherIcons(weather.weather[0].icon)" width="30%" />
            <span
              ><p class="temp">{{ parseInt(weather.main.temp) }}°C</p>
            </span>
          </li>
        </ul>
      </div>
      <div class="box">
        <h4>{{ getDate(2) }}</h4>

        <ul>
          <li
            class="list"
            v-for="weather in getDateWeather(2)"
            :key="weather.dt"
          >
            <p>
              {{ weather.dt_txt }}
            </p>
            <p>
              Weather: {{ weather.weather[0].main }} -
              {{ weather.weather[0].description }}
            </p>
            <img :src="getWeatherIcons(weather.weather[0].icon)" width="30%" />
            <span
              ><p class="temp">{{ parseInt(weather.main.temp) }}°C</p>
            </span>
          </li>
        </ul>
      </div>
      <div class="box">
        <h4>{{ getDate(3) }}</h4>

        <ul>
          <li
            class="list"
            v-for="weather in getDateWeather(3)"
            :key="weather.dt"
          >
            <p>
              {{ weather.dt_txt }}
            </p>
            <p>
              Weather: {{ weather.weather[0].main }} -
              {{ weather.weather[0].description }}
            </p>
            <img :src="getWeatherIcons(weather.weather[0].icon)" width="30%" />
            <span
              ><p class="temp">{{ parseInt(weather.main.temp) }}°C</p>
            </span>
          </li>
        </ul>
      </div>
      <div class="box">
        <h4>{{ getDate(4) }}</h4>

        <ul>
          <li
            class="list"
            v-for="weather in getDateWeather(4)"
            :key="weather.dt"
          >
            <p>
              {{ weather.dt_txt }}
            </p>
            <p>
              Weather: {{ weather.weather[0].main }} -
              {{ weather.weather[0].description }}
            </p>
            <img :src="getWeatherIcons(weather.weather[0].icon)" width="30%" />
            <span
              ><p class="temp">{{ parseInt(weather.main.temp) }}°C</p>
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      weathers: [],
      location: "Malmo",
    };
  },
  mounted() {
    axios
      .get(
        "https://api.openweathermap.org/data/2.5/forecast?q=" +
          this.location +
          "&appid=05247a6e758a20ba8486a5bc176af258&&mode=json&units=metric"
      )
      .then((res) => {
        console.log(res.data);
        this.weathers = res.data.list;
      });
  },
  methods: {
    getWeatherIcons(weatherIcons) {
      return "http://openweathermap.org/img/wn/" + weatherIcons + "@2x.png";
    },
    getDate(index) {
      let dateTemp = new Date();
      dateTemp.setDate(dateTemp.getDate() + index);

      var date =
        dateTemp.getFullYear() +
        "-" +
        (dateTemp.getMonth() + 1) +
        "-" +
        dateTemp.getDate();
      return date;
    },
    updateLocation() {
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/forecast?q=" +
            this.location +
            "&appid=05247a6e758a20ba8486a5bc176af258&&mode=json&units=metric"
        )
        .then((res) => {
          console.log(res.data);
          this.weathers = res.data.list;
        });
    },

    getDateWeather(index) {
      let dateTemp = new Date();
      dateTemp.setDate(dateTemp.getDate() + index);

      return this.weathers.filter((weather) => {
        return (
          new Date(weather.dt_txt).toDateString() === dateTemp.toDateString()
        );
      });
    },
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  background-image: url("https://shiftyjelly.files.wordpress.com/2013/11/w.jpg?w=1024&h=581");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

  & input {
    color: aliceblue;
    padding: 1%;
    width: 25%;
    background-color: rgba(250, 235, 215, 0.459) !important;
  }

  & button {
    padding: 1%;
  }

  & h1 {
    padding-top: 5%;
  }

  & h2 {
    padding-top: 3%;
  }

  & h4 {
    padding-top: 10%;
  }
}

.weather-title {
  text-align: center;
  color: aliceblue;
}

.weather__boxes {
  width: 100%;
  padding-top: 10%;
  padding-bottom: 10%;
  display: flex;
  flex-direction: row;
  align-content: space-around;
  justify-content: space-around;
}

.box {
  text-align: center;
  color: brown;
  width: 19%;
  background-color: rgb(250, 235, 215);
  border-style: ridge;
  border-color: 0 0 0 1px rgba(0, 0, 0, 0.219);
  border-radius: 50px;
  font-size: 13px;
  text-align: center;

  & ul {
    list-style-type: none;
  }

  & .temp {
    font-size: 25px;
  }
}

.list {
  border: 0.2px;
  border-style: none;
  border: 50px;
  background-color: rgba(250, 235, 215, 0.63);
}
</style>