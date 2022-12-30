<script setup>
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import Result from "../components/Result.vue";
import { useRoute } from "vue-router";
import { ref, watch, computed } from "vue";
import quizes from "../data/data.json";

const route = useRoute();

const quizId = parseInt(route.params.id);

const quiz = quizes.find((quiz) => quiz.id === quizId);

const currentQuestionIndex = ref(0);
const numberOfCorrectAns = ref(0);
const showResults = ref(false);
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

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    numberOfCorrectAns.value++;
  }
  //the length starts at 1, question index starts at 0
  //minus one to keep them in sync
  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showResults.value = true;
  }

  currentQuestionIndex.value++;
};
</script>
<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
      />
      <Result
        v-else
        :quizQuestionLength="quiz.questions.length"
        :numberOfCorrectAns="numberOfCorrectAns"
      />
    </div>
  </div>
</template>
