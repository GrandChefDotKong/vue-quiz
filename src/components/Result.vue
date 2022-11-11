<template>
  <div class="result">
    <h1>You results</h1>
    <p>
      {{ numberOfCorrectAnswers }} correct answers
      on {{ numberOfQuestions }} questions.
    </p>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

  const { numberOfCorrectAnswers, numberOfQuestions } = 
  defineProps(['numberOfCorrectAnswers', 'numberOfQuestions']);

</script>

<style scoped>
 .result {
  text-align: center;
  padding: 100px 0;
 }
 p {
  font-size: 25px;
 }
 h1 {
  font-size: 60px;
 }
</style>