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
        <div class="weather-report">
          <div class="map"></div>
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
      apiKey : `ee3bba6819aef1d1483bc23374dd04a6`,
      lat: null,
      lng: null,
      apiUrl : `https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}&lon=${this.lng}&appid=${this.apiKey}`
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
          console.log(response.data)
        })
        .catch(err => {
          console.log(err.message)
        })

        // Showing the Location on the map
        let latlon = this.lat + ',' + this.lng
        let img_url = "https://maps.googleapis.com/maps/api/staticmap?center="+latlon+"&zoom=14&size=400x300&sensor=false&key=YOUR_KEY";

        document.getElementById("mapholder").innerHTML = "<img src='"+img_url+"'>"
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
  padding: 10px 3%;
  max-width: 600px;
}

.home h2 {
  font-size: 2em;
}

.home .map {
  width: 300px;
  height: 200px;
}
</style>
