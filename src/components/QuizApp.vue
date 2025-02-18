<template>
    <div>
      <QuizQuestion
        v-for="(question, index) in questions"
        :key="index"
        :question="question"
        @answer-selected="handleAnswer"
      />
    </div>
  </template>
  
  <script>
  import QuizQuestion from './QuizQuestion.vue';
  
  export default {
    components: {
      QuizQuestion,
    },
    data() {
      return {
        questions: [
          {
            text: "What do plants need for photosynthesis?",
            options: [
              { text: "Oxygen & Sugar", isCorrect: false },
              { text: "Sunlight, Water & Carbon Dioxide", isCorrect: true },
              { text: "Protein & Soil", isCorrect: false },
            ],
          },
          {
            text: "Which gas do plants release during photosynthesis?",
            options: [
              { text: "Oxygen", isCorrect: true },
              { text: "Carbon Dioxide", isCorrect: false },
              { text: "Nitrogen", isCorrect: false },
            ],
          },
        ],
      };
    },
    methods: {
      handleAnswer(isCorrect) {
        this.$emit("update-points", isCorrect ? 10 : -5);
      },
    },
  };
  </script>

<style scoped>
.quiz-container {
  margin-top: 20px;
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

</style>