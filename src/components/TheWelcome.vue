<script setup></script>

<template>
  <div class="landing-page">
    <div class="name-wrapper">
      <div class="rohan-text">
        <p>Rohan</p>
      </div>
      <div class="desai-text">
        <p>Desai</p>
      </div>
    </div>
    <div class="swe-text">
      <p>&lt;Software Engineer&gt;</p>
    </div>
  </div>
</template>

<style scoped>
.landing-page {
  width: 100vw;
  height: 100vh;
}
.name-wrapper {
  position: absolute;
  margin-top: 100px;
  margin-left: -150px;
}

.rohan-text {
  font-family: 'Major Mono Display';
  font-size: 250px;
  height: 250px;
}

.desai-text {
  font-family: 'Major Mono Display';
  font-size: 250px;
  height: 250px;
  margin-left: 600px;
}

.swe-text {
  position: relative;
  font-family: 'Major Mono Display';
  font-style: italic;
  font-size: 30px;
  width: 500px;
  top: 300px;
  left: 850px;
}
</style>
