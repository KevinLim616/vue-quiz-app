<script setup>
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import { useRoute } from "vue-router";
import { ref, watch, computed } from "vue";
import quizes from "../data/data.json";

const route = useRoute();

const quizId = parseInt(route.params.id);

const quiz = quizes.find((quiz) => quiz.id === quizId);

const currentQuestionIndex = ref(0);

// const questionStatus = ref(
//   `${currentQuestionIndex.value}/${quiz.questions.length}`
// );

// watch(currentQuestionIndex, () => {
//   questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`;
// });

const questionStatus = computed(() => {
  return `${currentQuestionIndex.value}/${quiz.questions.length}`;
});

const barPercentage = computed(() => {
  return `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`;
});
</script>
<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question :question="quiz.questions[currentQuestionIndex]" />
    </div>
  </div>
  <button @click="currentQuestionIndex++">next</button>
</template>
