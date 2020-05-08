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
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      city: null,
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
</style>
