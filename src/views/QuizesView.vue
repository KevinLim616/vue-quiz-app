<script setup>
import quizesData from "../data/data.json";
import { ref, watch } from "vue";
import Card from "../components/Card.vue";
import gsap from "gsap";
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

//once we called the function with the hook
//vue will automaticly pass the element as a parameter
const beforeEnter = (element) => {
  //see this as card-enter-from
  element.style.opacity = 0;
  element.style.transform = "translateY(-100px)";
};

const enter = (element) => {
  //see this as card-enter-to
  gsap.to(element, {
    y: 0, // equivelent to transformY(0)
    opacity: 1,
    duration: 0.4,
    delay: element.dataset.index * 0.3,
  });
};
</script>
<template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
    <div class="options-container">
      <!--the props appear animate children upon render -->
      <TransitionGroup appear @before-enter="beforeEnter" @enter="enter">
        <Card
          v-for="(quiz, index) in quizes"
          :key="quiz.id"
          :quiz="quiz"
          :data-index="index"
        />
      </TransitionGroup>
    </div>
  </div>
</template>

<style scoped>
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

/* CARD animation*/
</style>
