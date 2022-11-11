<template>
  <div>
    <QuizHeader 
      :berPercentage="berPercentage" 
      :questionStatus="questionStatus"
    />
    <div v-if="!showResult">
      <Question 
        :question="quiz.questions[currentQuestionIndex]" 
        @selectOption="onOptionSelected"
      />
    </div>
    <div v-else>
      <Result 
        :numberOfCorrectAnswers="numberOfCorrectAnswers" 
        :numberOfQuestions="quiz.questions.length"
      />
    </div>
  </div>
</template>

<script setup>
import Question from '../components/Question.vue';
import QuizHeader from '../components/QuizHeader.vue';
import Result from '../components/Result.vue';
import quizes from '../data/quizes.json';
import { useRoute } from 'vue-router';
import { computed, ref } from 'vue';

  const route = useRoute();

  const quizId = parseInt(route.params.id);

  const quiz = quizes.find(quiz => quiz.id === quizId);
  const currentQuestionIndex = ref(0);
  const numberOfCorrectAnswers = ref(0);
  const showResult = ref(false);

  const onOptionSelected = (isCorrect) => {
    if(isCorrect) {
      numberOfCorrectAnswers.value++;
    }

    currentQuestionIndex.value++;

    if(currentQuestionIndex.value >= quiz.questions.length) {
      showResult.value = true;
    }
  }

  const questionStatus = 
    computed(() => `${ currentQuestionIndex.value }/${ quiz.questions.length }`);
  const berPercentage = 
    computed(() => `${ currentQuestionIndex.value / quiz.questions.length * 100 }%`);

</script>








