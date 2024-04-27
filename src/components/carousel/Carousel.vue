<template>
    <div class="carousel">
        <div class="carousel-inner">
            <carousel-indicators 
                :total="slides.length" 
                :current-slide="currentSlide" 
                @change-slide="$emit('change-slide', $event)"
                @click.native="stopSlideInterval"
            ></carousel-indicators>
            <carousel-item 
                v-for="(slide, index) in slides" 
                :slide="slide"
                :key="`item-${index}`"
                :current-slide="currentSlide"
                :index="index"
                @submit-date="$emit('submit-date', $event)"
                @submit-answer="$emit('submit-answer', $event)"
            ></carousel-item>
        </div>
    </div>
</template>

<script>
import CarouselItem from "./CarouselItem.vue";
import CarouselIndicators from "./CarouselIndicators.vue";
import CarouselNext from "./CarouselNext.vue";

export default {
    props: ['slides', 'currentSlide'],
    components: { CarouselItem , CarouselIndicators , CarouselNext },
    data: () => ({
        slideIntervalId: null,
        date: null,
    }),
    beforeUnmount() {
        clearInterval(this.slideIntervalId);
    },
    methods: {
        stopSlideInterval() {
            clearInterval(this.slideIntervalId);
        },
    },
};
</script>

<style scoped>
.carousel {
    display: flex;
    justify-content: center;
}
.carousel-inner {
    position: relative;
    width: 900px;
    height: 500px;
    overflow: hidden;
}
</style>