<script setup>
import quizesData from "./data/data.json";
import { ref, watch } from "vue";

//we have to store data into a state to perform search function
const quizes = ref(quizesData);
const search = ref("");

//watch() takes two parameters, first is the thing we wanna watch on
//and the second is a callback function
watch(search, () => {
  quizes.value = quizesData.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>
<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
    <div class="options-container">
      <div v-for="quize in quizes" :key="quize.id" class="card">
        <img :src="quize.img" :alt="quize.name + ' thumbnail'" />
        <div class="card-text">
          <h2>{{ quize.name }}</h2>
          <p>{{ quize.questions.length }} questions</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 1000px;
  margin: 0 auto;
}

header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

/* CARD */

.card {
  width: 310px;
  overflow: hidden;
  border-radius: 2%;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 35px;
  margin-right: 20px;
  cursor: pointer;
}

.card img {
  width: 100%;
  height: 190px;
  margin: 0;
}

.card .card-text {
  padding: 0 5px;
}

.card .card-text h2 {
  font-weight: bold;
}
</style>
