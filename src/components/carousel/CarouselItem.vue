<template>
    <div class="carousel-item" v-show="index === currentSlide">
      <img v-if="slide.image" :src="slide.image" alt="Slide image">
      <div v-else-if="slide.question">
        <p>{{ slide.question }}</p>
        <input v-if="slide.isAnswerInput" type="text" v-model="answer">
        <button v-if="slide.isAnswerInput" @click="submitAnswer">Submit Answer</button>
      </div>
      <div v-else-if="slide.isDateInput">
        <input type="date" v-model="date">
        <button @click="submitDate">Submit Date</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['slide', 'index', 'currentSlide'],
    data: () => ({
      date: null,
      answer: null,
    }),
    methods: {
      submitDate() {
        this.$emit('submit-date', this.date);
      },
      submitAnswer() {
        this.$emit('submit-answer', this.answer);
      },
    },
  };
  </script>
  
  <style scoped>
  .carousel-item {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  </style>