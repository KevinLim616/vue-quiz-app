<script setup>
import { RouterLink } from "vue-router";
const { numberOfCorrectAns, quizQuestionLength } = defineProps([
  "numberOfCorrectAns",
  "quizQuestionLength",
]);
</script>
<template>
  <div class="results">
    <p>Your Result...</p>
    <h1>{{ numberOfCorrectAns }} / {{ quizQuestionLength }}</h1>
    <RouterLink to="/">Go Back</RouterLink>
  </div>
</template>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0px;
}
p {
  font-size: 25px;
}
h1 {
  font-size: 80px;
}
</style>
