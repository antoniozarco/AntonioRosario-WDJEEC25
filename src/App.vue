<template>
  <div class="shadow-box">
    <div class="app-container">
      <div class="carousel-container">
        <carousel class="carousel-image" 
        :slides="slides" 
        :current-slide="currentSlide" 
        @submit-date="setDate" 
        @submit-answer="setAnswer"
        ></carousel>
        <carousel-indicators 
        :slides="slides" 
        :current-slide="currentSlide" 
        @select-slide="selectSlide" 
        @stopInterval="stopSlideInterval"
        ></carousel-indicators>
        <carousel-next 
        :moveSlide="moveSlide" 
        @stopInterval="stopSlideInterval"
        ></carousel-next>
      </div>
      <div class="answer-container">
        <p>{{ answer }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Carousel from "./components/carousel/Carousel.vue";
import CarouselIndicators from "./components/carousel/CarouselIndicators.vue";
import CarouselItem from "./components/carousel/CarouselItem.vue";
import CarouselNext from './components/carousel/CarouselNext.vue';

export default {
  name: "App",
  components: { Carousel , CarouselIndicators, CarouselItem, CarouselNext},
  data: () => ({
    slides: [
      { question: "Em que ano se deu a primeira edição das JEEC?", answer: "A primeira edição das JEEC foi em 2019.", isAnswerInput: true },
      { isDateInput: true },
      { image: require("../challenge2.png") },
      { image: require("../challenge.png") },
    ],
    date: null,
    answer: null,
    currentSlide: 0,
    slideIntervalId: null,
    ano: null,
  }),
  created() {
    this.startSlideInterval();
  },
  beforeUnmount(){
    clearInterval(this.slideIntervalId);
  },
  methods: {
    startSlideInterval(){
      this.slideIntervalId = setInterval(() => {
        this.moveSlide('next');
      }, 3000);
    },
    stopSlideInterval(){
      clearInterval(this.slideIntervalId);
    },
    setDate(date) {
      this.date = date;
      this.answer = `A data inserida foi ${date}.`;
    },
    setAnswer(ano) {
      this.ano = ano;
      if(ano == 2001){
        this.answer = `Correto.`;
      } else {
        this.answer = `O ano correto é 2001 e o submetido foi ${ano}.`;
      }
    },
    moveSlide(direction) {
      if (direction === 'next') {
        this.currentSlide++;
        if (this.currentSlide >= this.slides.length) {
          this.currentSlide = 0; 
        }
      } else if (direction === 'prev') {
        this.currentSlide--;
        if (this.currentSlide < 0) {
          this.currentSlide = this.slides.length - 1;
        }
      }
    },
    selectSlide(index){
      this.stopSlideInterval();
      this.currentSlide = index;
    },
  },
};
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.carousel-container {
  margin-top: 50px;
}

.carousel-container p {
  margin-top: 50px;
  text-align: center;
}

.carousel-image img {
  object-fit: cover;
  object-position: center;
  width: 900px;
  height: 500px;
}

.answer-container {
  margin-top: 20px;
  text-align: center;
}

.shadow-box {
  box-shadow: 0px 0px 5px 5px rgba(0, 0, 0, 0.1);
}
</style>