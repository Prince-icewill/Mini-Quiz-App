<template>
  <div class="drag-drop-container">
    <h2 class="section-title">Drag and Drop the Correct Answers</h2>
    <div class="questions-container">
      <div v-for="(question, qIndex) in questions" :key="qIndex" class="question-card">
        <p class="question-text">{{ question.text }}</p>
        <div
          class="drop-zone"
          :class="{ correct: question.isCorrect, incorrect: question.isIncorrect }"
          @drop="handleDrop($event, qIndex)"
          @dragover.prevent
          @dragenter.prevent
        >
          <span v-if="question.droppedAnswer">{{ question.droppedAnswer }}</span>
          <span v-else class="placeholder">Drop here</span>
        </div>
      </div>
    </div>

    <div class="answers-container">
      <div
        v-for="(answer, aIndex) in answers"
        :key="aIndex"
        class="answer-card"
        :draggable="true"
        @dragstart="startDrag($event, answer)"
      >
        {{ answer.text }}
      </div>
    </div>

    <button class="restart-btn" @click="restartGame">Restart</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const questions = ref([
  { text: "What is the process by which plants make their own food?", correctAnswer: "Photosynthesis", droppedAnswer: "", isCorrect: false, isIncorrect: false },
  { text: "Which gas do plants absorb for photosynthesis?", correctAnswer: "Carbon Dioxide", droppedAnswer: "", isCorrect: false, isIncorrect: false },
]);

const answers = ref([
  { text: "Photosynthesis" },
  { text: "Carbon Dioxide" },
  { text: "Oxygen" },
  { text: "Respiration" },
]);

const startDrag = (event, answer) => {
  event.dataTransfer.setData("text", answer.text);
};

const handleDrop = (event, qIndex) => {
  const droppedText = event.dataTransfer.getData("text");
  const question = questions.value[qIndex];

  if (droppedText === question.correctAnswer) {
    question.isCorrect = true;
    question.isIncorrect = false;
  } else {
    question.isIncorrect = true;
    question.isCorrect = false;
  }

  question.droppedAnswer = droppedText;
};

const restartGame = () => {
  questions.value.forEach((q) => {
    q.droppedAnswer = "";
    q.isCorrect = false;
    q.isIncorrect = false;
  });
};
</script>

<style scoped>
.drag-drop-container {
  max-width: 600px;
  margin: auto;
  padding: 20px;
  text-align: center;
}

.section-title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 15px;
}

.questions-container {
  margin-bottom: 20px;
}

.question-card {
  background: #f9f9f9;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.question-text {
  font-weight: bold;
}

.drop-zone {
  height: 40px;
  line-height: 40px;
  margin-top: 10px;
  background: #eee;
  border: 2px dashed #aaa;
  border-radius: 5px;
}

.drop-zone.correct {
  background: lightgreen;
  border-color: green;
}

.drop-zone.incorrect {
  background: lightcoral;
  border-color: red;
}

.placeholder {
  color: gray;
  font-style: italic;
}

.answers-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.answer-card {
  background: #6200ea;
  color: white;
  padding: 10px 15px;
  margin: 5px;
  cursor: grab;
  border-radius: 5px;
}

.restart-btn {
  margin-top: 20px;
  padding: 10px;
  background: #6200ea;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}
</style>
