<template>
    <div class="carousel-item" v-for="slide in slides">
        <img :src="slide"/>
    </div>
</template>

<script>
export default {
    props:['slide'],
};
</script>