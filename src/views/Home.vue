<template>
  <div class="home">
    <div class="card">
      <div class="card-title">
        <h2 class="teal-text center">Vue Weather</h2>
      </div>
      <div class="card-content">
        <form>
          <div class="field">
            <label for="location">Enter the city</label>
            <input type="text" name="location" v-model="city" placeholder="Enter the city name...">
          </div>
        </form>
      </div>
      <div class="card-footer">
        <div class="location-info">
          <p class="center">You are currently at:</p>
          <p class="teal-text center">{{ location }}</p>
        </div>
      </div>
      <div class="card-footer" >
        <p class="teal-text center">Report for your location:</p>
        <div class="weather-report">
          <table class="striped">
            <thead>
              <tr>
                  <th>Key</th>
                  <th>Value</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Date</td>
                <td>{{ weather.dt }}</td>
              </tr>
              <tr>
                <td>Weather</td>
                <td>{{ weather.weather[0].main }} - {{ weather.weather[0].description }}</td>
              </tr>
              <tr>
                <td>City</td>
                <td>{{ weather.name }}</td>
              </tr>
              <tr>
                <td>Country</td>
                <td>{{ weather.sys.country }}</td>
              </tr>
              <tr>
                <td>Sunrise</td>
                <td>{{ weather.sys.sunrise }}</td>
              </tr>
              <tr>
                <td>Sunset</td>
                <td>{{ weather.sys.sunset }}</td>
              </tr>
              <tr>
                <td>Temerature</td>
                <td>{{ weather.main.temp }}</td>
              </tr>
              <tr>
                <td>Feels Like</td>
                <td>{{ weather.main.feels_like }}</td>
              </tr>
              <tr>
                <td>Min Temperature</td>
                <td>{{ weather.main.temp_min }}</td>
              </tr>
              <tr>
                <td>Max Temperature</td>
                <td>{{ weather.main.temp_max }}</td>
              </tr>
              <tr>
                <td>Pressure</td>
                <td>{{ weather.main.pressure }}</td>
              </tr>
              <tr>
                <td>Humidity</td>
                <td>{{ weather.main.humidity }}</td>
              </tr>
              <tr>
                <td>Sea Level</td>
                <td>{{ weather.main.sea_level }} m</td>
              </tr>
              <tr>
                <td>Ground Level</td>
                <td>{{ weather.main.grnd_level }} m</td>
              </tr>
              <tr>
                <td>Wind Speed</td>
                <td>{{ weather.wind.speed }}</td>
              </tr>
              <tr>
                <td>Wind Direction</td>
                <td>{{ weather.wind.deg }} degree</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Home',
  data() {
    return {
      city: null,
      apiKey : `ee3bba6819aef1d1483bc23374dd04a6`, // Api key for open weather
      lat: null,
      lng: null,
      location: null,
      weather: null
    }
  },
  created() {

    // Finding lattitude and longitude of current location
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(position => {
        this.lat = position.coords.latitude
        this.lng = position.coords.longitude

        // Getting weather data
        axios.get(`https://api.openweathermap.org/data/2.5/weather?lat=${position.coords.latitude}&lon=${position.coords.longitude}&appid=${this.apiKey}`)
        .then(response => {
          this.weather = response.data
        })
        .catch(err => {
          console.log(err.message)
        })

        // Showing the Location name
        axios.get(`https://api.opencagedata.com/geocode/v1/json?q=${this.lat}+${this.lng}&key=3ffd64246ea74371ad9476adabd3c0a4`)
        .then(response => {
          this.location = response.data.results[0].formatted
        })
        .catch(err => {
          console.log(err.message)
        })

      })
    } else {
      alert("Could not get Location. Please Try again.")
    }
  }
}
</script>

<style>
.home {
  display: flex;
  justify-content: center;
}

.home .card {
  max-width: 600px;
  min-width: 300px;
}

.home h2 {
  font-size: 2em;
}

.home .card-footer {
  border-bottom: 1px solid #d4d9d1;
  padding: 10px 4%;
}
</style>
