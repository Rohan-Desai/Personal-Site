<script setup>
import { defineProps } from 'vue'

// eslint-disable-next-line no-unused-vars
const props = defineProps({
  skill: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="skill-button">
    <p>{{ skill }}</p>
  </div>
</template>

<style scoped>
.skill-button {
  display: inline-block;
  padding: 8px 12px;
  margin: 4px;
  background-color: #e0e0e0; /* Light grey background */
  color: #333; /* Text color */
  font-family: Adamina;
  border-radius: 20px; /* Rounded corners */
  font-size: 1vw; /* Font size */
  text-align: center;
  font-weight: bold;
  border: 0px;
}
@media (min-width: 2400px) {
  .skill-button {
    padding: 12px 20px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: 1.2vw; /* Font size */
  }
}
@media (max-width: 2400px) and (min-width: 1800px) {
  .skill-button {
    padding: 12px 20px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: .9vw; /* Font size */
  }
}
@media (max-width: 1800px) and (min-width: 1600px) {
  .skill-button {
    padding: 12px 20px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: .9vw; /* Font size */
  }
}
@media (max-width: 1600px) and (min-width: 1380px) {
  .skill-button {
    padding: 10px 18px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: .9vw; /* Font size */
  }
}
@media (max-width: 1380px) and (min-width: 850px) {
  .skill-button {
    padding: 8px 12px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: .9vw; /* Font size */
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .skill-button {
    padding: 5px 10px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: 1.4vw; /* Font size */
  }
}
@media (max-width: 500px) {
  .skill-button {
    padding: 3px 7px;
    margin: 4px;
    border-radius: 50px; /* Rounded corners */
    font-size: 1.8vw; /* Font size */
  }
}
</style>
