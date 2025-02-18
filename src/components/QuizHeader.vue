<template>
    <div class="quiz-header">
      <span>🎯 Goal: {{ goal }} points</span>
      <span>Current Points: {{ points }}</span>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      goal: Number,
      points: Number,
    },
  };
  </script>
  
  <style scoped>
  .quiz-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #69007f;
    color: white;
    padding: 15px;
    font-size: 16px;
    font-weight: 600;
    border-radius: 8px;
    margin-bottom: 20px;
  }
  </style>
  