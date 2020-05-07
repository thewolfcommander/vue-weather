<template>
  <div class="about">
    <h1 class="center teal-text">About Me</h1>

    <p class="center dark-grey-text">I am Manoj Tyagi. I am a full-stack developer. I am currently in my pre-final year of Undergraduation. I have experience in working with Django.</p>
  </div>
</template>

<script>
export default {
  name: 'About',
  data() {
    return {

    }
  }
}
</script>


<style>
.about {
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.about p {
  max-width: 550px;
  font-size: 1.2em
}
</style>