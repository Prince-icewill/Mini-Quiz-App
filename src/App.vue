<template>
  <div class="quiz-app">
    <QuizHeader :goal="30" :points="currentPoints" />

    <div class="quiz-container">
      <QuizQuestion
        v-for="(question, index) in questions"
        :key="index"
        :question="question"
        @answer-selected="handleAnswer"
      />
    </div>

    <DragAndDropSection />

    <button class="continue-btn">Continue →</button>
  </div>
</template>

<script>
import QuizHeader from "./components/QuizHeader.vue";
import QuizQuestion from "./components/QuizQuestion.vue";
import DragAndDropSection from "./components/DragAndDropSection.vue";

export default {
  components: { QuizHeader, QuizQuestion, DragAndDropSection },
  data() {
    return {
      currentPoints: 5,
      questions: [
        {
          id: 1,
          text: "What do plants need for photosynthesis?",
          options: [
            { text: "Oxygen & Sugar", isCorrect: false },
            { text: "Sunlight, Water & Carbon Dioxide", isCorrect: true },
            { text: "Protein & Soil", isCorrect: false },
          ],
          selected: null,
        },
        {
          id: 2,
          text: "Which gas do plants release during photosynthesis?",
          options: [
            { text: "Oxygen", isCorrect: true },
            { text: "Carbon Dioxide", isCorrect: false },
            { text: "Nitrogen", isCorrect: false },
          ],
          selected: null,
        },
      ],
    };
  },
  methods: {
    handleAnswer({isCorrect }) {
      if (isCorrect) {
        this.currentPoints += 10;
      } else {
        this.currentPoints -= 5;
      }
    },
  },
};
</script>

<style scoped>
.quiz-app {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  font-family: "Inter", sans-serif;
}

.quiz-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.continue-btn {
  background: #69007f;
  color: white;
  width: 100%;
  padding: 12px;
  font-size: 16px;
  font-weight: bold;
  border: none;
  border-radius: 8px;
  margin-top: 20px;
  cursor: pointer;
  transition: 0.3s;
}

.continue-btn:hover {
  background: #520067;
}
</style>
