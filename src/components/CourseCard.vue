<script setup>
import { ref, onMounted } from 'vue'
import coursesData from '/src/components/courses.json'
import SkillButton from '/src/components/SkillButton.vue'

const courses = ref([])
const selectedCourse = ref(null)

onMounted(() => {
  courses.value = coursesData.courses
})

const showModal = (course) => {
  selectedCourse.value = course
}

const closeModal = () => {
  selectedCourse.value = null
}
</script>
<template>
  <div class="container">
    <div v-for="course in courses" :key="course.title" class="card" @click="showModal(course)">
      <h1>{{ course.title }}</h1>
      <p>{{ course.name }}</p>
    </div>
    <transition name="fade">
      <div v-if="selectedCourse" class="modal-overlay" @click="closeModal">
        <div class="modal-content" @click.stop>
          <h2>{{ selectedCourse.title }}</h2>
          <h3>{{ selectedCourse.name }}</h3>
          <hr />
          <p>{{ selectedCourse.description }}</p>
          <div class="tags-wrapper">
            <div class="tags">
              <span v-for="tag in selectedCourse.skills" :key="tag" class="tag">
                <SkillButton :skill="tag" />
              </span>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 4 columns */
  grid-template-rows: repeat(3, 1fr); /* 3 rows */
  gap: 45px;
  justify-items: center;
  align-items: center;
  margin: 0px auto;
  width: 70%;
  height: 70vh; /* Ensure the container takes full viewport height */
}

.card {
  background-color: #f9f9f9;
  color: black;
  border: 1px solid #ccc;
  border-radius: 35px; /* Rounded corners */
  padding: 16px;
  width: 225px; /* Set fixed width */
  height: 225px; /* Set fixed height */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.2s ease;
}

.card:hover {
  opacity: 0.8;
  transform: scale(1.1);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.card h1 {
  margin: 0 0 8px;
  font-weight: 800;
  font-size: 1.8em; /* Adjust font size */
}

.card p {
  margin: 0;
  font-size: 1.1em; /* Adjust font size */
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: #2f2f2f;
  color: white;
  border-radius: 40px;
  width: 50%;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.modal-content h2,
.modal-content h3 {
  text-align: center;
}

.modal-content h2 {
  font-size: 2.5vw;
  font-weight: 700;
  margin-top: 20px;
}

.modal-content h3 {
  font-size: 1vw;
}

hr {
  margin: 10px auto; /* Center horizontally */
  width: 50%;
  align-items: center;
}

.modal-content p {
  margin: 0px 50px;
  font-size: 0.8vw;
}

.tags {
  margin: 20px;
}

.skill-button {
  padding: 7px 10px;
  margin: 6px;
  border-radius: 50px; /* Rounded corners */
  font-size: 0.7vw; /* Font size */
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to,
.fade-leave-active {
  opacity: 0;
}

@media (min-width: 1800px) {
  .card {
    padding: 16px;
    width: 300px; /* Set fixed width */
    height: 300px; /* Set fixed height */
  }

  .card h1 {
    margin: 0 0 20px;
    font-weight: 800;
    font-size: 2.5em; /* Adjust font size */
  }

  .card p {
    font-size: 1.5em; /* Adjust font size */
  }

  .modal-content h2 {
    font-size: 3vw;
  }

  .modal-content h3 {
    font-size: 1.5vw;
  }

  hr {
    margin: 30px auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 50px;
    font-size: 1vw;
  }

  .tags {
    margin: 30px;
  }

  .skill-button {
    padding: 10px 20px;
    margin: 10px;
    border-radius: 50px; /* Rounded corners */
    font-size: 0.8vw; /* Font size */
  }
}
@media (max-width: 1600px) and (min-width: 1380px) {
  .card {
    padding: 16px;
    width: 200px; /* Set fixed width */
    height: 200px; /* Set fixed height */
  }

  .card h1 {
    margin: 0 0 20px;
    font-weight: 800;
    font-size: 1.3em; /* Adjust font size */
  }

  .card p {
    font-size: 1em; /* Adjust font size */
  }
  .modal-content h2 {
    font-size: 4vw;
  }

  .modal-content h3 {
    font-size: 1.5vw;
  }

  hr {
    margin: 20px auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 50px;
    font-size: 1.1vw;
  }

  .tags {
    margin: 20px;
  }

  .skill-button {
    padding: 7px 15px;
    margin: 7px;
    font-size: 0.8vw; /* Font size */
  }
}
@media (max-width: 1380px) and (min-width: 1100px) {
  .container {
    gap: 20px;
  }
  .card {
    padding: 16px;
    width: 175px; /* Set fixed width */
    height: 175px; /* Set fixed height */
  }

  .card h1 {
    margin: 0 0 7px;
    font-weight: 800;
    font-size: 1.2em; /* Adjust font size */
  }

  .card p {
    font-size: 0.8em; /* Adjust font size */
  }
  .modal-content h2 {
    font-size: 4vw;
  }

  .modal-content h3 {
    font-size: 1.5vw;
  }

  hr {
    margin: 20px auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 50px;
    font-size: 1.1vw;
  }

  .tags {
    margin: 20px;
  }

  .skill-button {
    padding: 6px 12px;
    margin: 6px;
    font-size: 0.8vw; /* Font size */
  }
}
@media (max-width: 1100px) and (min-width: 900px) {
  .container {
    gap: 15px;
  }
  .card {
    padding: 16px;
    width: 150px; /* Set fixed width */
    height: 150px; /* Set fixed height */
  }

  .card h1 {
    margin: 0 0 7px;
    font-size: 1em; /* Adjust font size */
  }

  .card p {
    font-size: 0.7em; /* Adjust font size */
  }
  .modal-content h2 {
    font-size: 4vw;
  }

  .modal-content h3 {
    font-size: 1.5vw;
  }

  hr {
    margin: 15px auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 50px;
    font-size: 1.1vw;
  }

  .tags {
    margin: 20px;
  }

  .skill-button {
    padding: 5px 10px;
    margin: 5px;
    font-size: 0.8vw; /* Font size */
  }
}
@media (max-width: 900px) and (min-width: 650px) {
  .container {
    overflow-y: auto;
    grid-template-columns: repeat(2, 1fr); /* 4 columns */
    grid-template-rows: repeat(6, 1fr); /* 3 rows */
    gap: 10px;
    width: 90%;
  }
  .card h1 {
    margin: 0 0 7px;
    font-size: 1em; /* Adjust font size */
  }

  .card p {
    font-size: 0.8em; /* Adjust font size */
  }
  .modal-content h2 {
    font-size: 3vw;
  }

  .modal-content h3 {
    font-size: 1.2vw;
  }

  hr {
    margin: 10 auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 30px;
    font-size: 0.8vw;
  }

  .tags {
    margin: 7px 15px;
  }

  .skill-button {
    padding: 2px 4px;
    margin: 1px 3px;
    font-size: 0.8vw; /* Font size */
  }
}
@media (max-width: 650px) and (min-width: 500px) {
  .container {
    overflow-y: auto;
    grid-template-columns: repeat(2, 1fr); /* 4 columns */
    grid-template-rows: repeat(6, 1fr); /* 3 rows */
    gap: 10px;
    width: 90%;
  }
  .card {
    padding: 16px;
    width: 175px; /* Set fixed width */
    height: 175px; /* Set fixed height */
  }
  .card h1 {
    margin: 0 0 7px;
    font-size: 1em; /* Adjust font size */
  }

  .card p {
    font-size: 0.7em; /* Adjust font size */
  }
  .modal-content h2 {
    font-size: 3vw;
  }

  .modal-content h3 {
    font-size: 1.2vw;
  }

  hr {
    margin: 10 auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 30px;
    font-size: 0.8vw;
  }

  .tags {
    margin: 7px 15px;
  }

  .skill-button {
    padding: 2px 4px;
    margin: 1px 3px;
    font-size: 0.8vw; /* Font size */
  }
}
@media (max-width: 500px) {
  .container {
    overflow-y: auto;
    grid-template-columns: repeat(1, 1fr); /* 4 columns */
    grid-template-rows: repeat(12, 1fr); /* 3 rows */
    gap: 10px;
    width: 90%;
  }
  .card h1 {
    margin: 0 0 7px;
    font-size: 1em; /* Adjust font size */
  }

  .card p {
    font-size: 0.7em; /* Adjust font size */
  }
  .modal-content h2 {
    font-size: 3vw;
  }

  .modal-content h3 {
    font-size: 1.2vw;
  }

  hr {
    margin: 10 auto; /* Center horizontally */
    width: 50%;
    align-items: center;
  }

  .modal-content p {
    margin: 0px 30px;
    font-size: 0.8vw;
  }

  .tags {
    margin: 15px;
  }

  .skill-button {
    padding: 2px 4px;
    margin: 1px 3px;
    font-size: 0.8vw; /* Font size */
  }
}
</style>
