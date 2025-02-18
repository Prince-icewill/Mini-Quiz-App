<template>
    <p :class="{ correct: isCorrect, incorrect: !isCorrect }">
      {{ isCorrect ? "✅ Correct!" : "❌ Think again! Consider the key factors." }}
    </p>
  </template>
  
  <script>
  export default {
    props: {
      isCorrect: Boolean,
    },
  };
  </script>
  
  <style scoped>
.feedback {
  padding: 10px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
  border-radius: 4px;
  font-size: 16px;
}

.correct {
  background: green;
  color: white;
}

.incorrect {
  background: red;
  color: white;
}

  </style>
  