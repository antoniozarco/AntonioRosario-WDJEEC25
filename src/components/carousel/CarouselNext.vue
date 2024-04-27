<template>
    <div class="carousel-move">
        <div class="carousel-sides">
            <div class="left">
                <button class="carousel_box-button" @click="handleClick('prev')">Previous</button>
            </div>
            <div class="right">
                <button class="carousel_box-button" @click="handleClick('next')">Next</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['moveSlide'],
    methods: {
        handleClick(direction) {
            this.$emit('stopInterval');
            this.moveSlide(direction);
        }
    }
};
</script>

<style scoped>
.carousel-move {
    display: flex;
    justify-content: center;
    margin-top: 50px;
}
.carousel-sides {
    display: flex;
}
.left {
    margin-right: 15px;
}
.carousel_box-button {
    background-color: #f1f1f1;
    border: none;
    color: black;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
}
.carousel_box-button:hover {
    background-color: #ddd;
}
</style>
