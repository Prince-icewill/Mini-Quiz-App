<template>
  <div class="question-container">
    <h2 class="question-title">{{ question.text }}</h2>

    <div
      v-for="(option, index) in localOptions"
      :key="index"
      :class="['answer-option', selectedAnswer === option.text ? (option.isCorrect ? 'correct' : 'incorrect') : '']"
      @click="selectAnswer(option)"
    >
      {{ option.text }}
    </div>

    <p v-if="selectedAnswer" :class="['feedback-message', isCorrect ? 'correct' : 'incorrect']">
      {{ isCorrect ? "✅ Right!" : "❌ Think again!" }}
    </p>

    <button class="reset-btn" @click="resetSelection">Change Answer</button>
  </div>
</template>

<script>
export default {
  props: {
    question: Object,
  },
  data() {
    return {
      selectedAnswer: null,
      isCorrect: null,
      localOptions: JSON.parse(JSON.stringify(this.question.options)),
    };
  },
  methods: {
    selectAnswer(option) {
      this.selectedAnswer = option.text;
      this.isCorrect = option.isCorrect;
      this.$emit("answer-selected", { questionId: this.question.id, isCorrect: option.isCorrect });
    },
    resetSelection() {
      this.selectedAnswer = null;
      this.isCorrect = null;
    },
  },
};
</script>

<style scoped>
.question-container {
  background: #fff;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.question-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 15px;
}

.answer-option {
  background: #f5f5f5;
  padding: 12px;
  border-radius: 8px;
  cursor: pointer;
  margin-bottom: 10px;
  transition: background 0.3s ease, transform 0.2s ease;
}

.answer-option:hover {
  background: #e0e0e0;
}

.correct {
  background: #e6f8e0 !important;
  border: 2px solid #4caf50;
  color: #2e7d32;
}

.incorrect {
  background: #fdecea !important;
  border: 2px solid #f44336;
  color: #c62828;
}

.feedback-message {
  margin-top: 10px;
  font-weight: bold;
  padding: 10px;
  border-radius: 5px;
  display: inline-block;
}

.feedback-message.correct {
  color: #2e7d32;
  background: #e6f8e0;
}

.feedback-message.incorrect {
  color: #c62828;
  background: #fdecea;
}

.reset-btn {
  margin-top: 15px;
  margin-left: 20px;
  padding: 8px 12px;
  border: none;
  border-radius: 5px;
  background: #6200ea;
  color: white;
  cursor: pointer;
  transition: 0.3s ease;
}

.reset-btn:hover {
  background: #3700b3;
}
</style>
