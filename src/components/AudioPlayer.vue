<script setup>
import { ref } from 'vue'

const audioFiles = ref([
  { name: 'Track 1', src: '@/assets/track1.mp3' },
  { name: 'Track 2', src: '@/assets/track2.wav' }
])

const audio = ref(new Audio())
const isPlaying = ref(false)
const volume = ref(1.0)

const playAudio = (src) => {
  if (audio.value.src !== src) {
    audio.value.src = src
    audio.value.load()
  }
  audio.value.play()
  isPlaying.value = true
}

const pauseAudio = () => {
  audio.value.pause()
  isPlaying.value = false
}

const stopAudio = () => {
  audio.value.pause()
  audio.value.currentTime = 0
  isPlaying.value = false
}

const changeVolume = (event) => {
  volume.value = event.target.value
  audio.value.volume = volume.value
}
</script>
<template>
  <div class="audio-player">
    <div v-for="(file, index) in audioFiles" :key="index" class="audio-file">
      <button @click="playAudio(file.src)" :disabled="isPlaying && audio.value.src === file.src">
        Play {{ file.name }}
      </button>
    </div>
    <button @click="pauseAudio" :disabled="!isPlaying">Pause</button>
    <button @click="stopAudio">Stop</button>
    <label for="volume">Volume</label>
    <input
      type="range"
      id="volume"
      min="0"
      max="1"
      step="0.01"
      v-model="volume"
      @input="changeVolume"
    />
  </div>
</template>
<style scoped>
.audio-player {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.audio-file {
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  cursor: pointer;
}

label {
  margin-right: 10px;
}

input[type='range'] {
  width: 100%;
}
</style>
