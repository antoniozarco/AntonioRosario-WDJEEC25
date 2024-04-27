<template>
    <div class="carousel-indicators">
      <button 
        v-for="(slide, index) in slides" 
        :key="index" 
        @click="selectSlide(index)"
        :class="{ active: index === currentSlide }"
      ></button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['slides', 'currentSlide'],
    methods: {
      selectSlide(index) {
        clearInterval(this.slideIntervalId);
        this.$emit('select-slide', index);
      },
    },
  };
  </script>

<style scoped>
.carousel-indicators {
  position: absolute;
  transform: translateX(-50%);
  left: 50%;
  margin-top: 15px;
}

.carousel-indicators button {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: #ccc;
  border: none;
  margin: 1px;
  cursor: pointer;
}

.carousel-indicators button.active {
  background-color: #333;
}
</style>