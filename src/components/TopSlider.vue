<template>
    <div class="slider">
        <div class="slider__wrapper">
            <div class="slider__img" 
                v-for="slide in slides" 
                :key="slide.id" 
                :style="{transform: `translateX(-${100 * activeSlide}%)`}"
            >
                <img :src="slide.img" alt="">
                <h1 class="slider__header">{{slide.text}}</h1>
            </div>
        </div>
        <div class="slider__button" 
            v-text="'<'"
            @click="$emit('decrement')"
        >
        </div>
        <div class="slider__button slider__button_next"
            @click="$emit('increment')"
        >
            >
        </div>
        <div class="slider__counter">
            <div 
                :class="i-1 == activeSlide ? 'counter__item counter__item-active ' : 'counter__item'" 
                v-for="i in lengthSlider" 
                :key="i"
                @click="$emit('setActive', i)"
            >
                <template v-if="i-1 == activeSlide">
                    <span class="count__progress" :style="{width: `${timer / 100}%`}"></span>
                    {{i}}
                </template>

                <template v-else>
                    {{i}}
                </template>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "TopSlider",
        props: ["slides", "activeSlide", "timer"],

        computed: {
            lengthSlider() {
                return this.slides.length 
            }
        }
    }
</script>


<style scoped>
    .slider {
        width: 100%;
        height: 300px;
        background: green;
        position: relative;
        z-index: 1
    }

    .slider__wrapper {
        width: 100%;
        height: 100%;
        display: flex;
        overflow: hidden;
    }

    .slider__img {
        min-width: 100%;
        width: 100%;
        height: 300px;
        transition: .5s ease-in;
    }

    .slider__img img {
        width: 100%;
        height: 100%;
    }

    .slider__header {
        color: #fff;
        position: absolute;
        top: 20px;
        left: 50px
    }

    .slider__button {
        width: 30px;
        height: 50px;
        background: #000;
        position: absolute;
        top: calc(50% - 25px);
        color: #fff;
        display: flex;
        justify-content: center;
        align-items: center;
        font-weight: bold;
        cursor: pointer;
    }

    .slider__button:hover {
        opacity: .5;
    }

    .slider__button_next {
        right: 0
    }

    .slider__counter {
        width: 200px;
        height: 30px;
        background: green;
        position: absolute;
        bottom: 10px;
        left: calc(50% - 100px);
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;
    }

    .counter__item {
        width: 20px;
        height: 20px;
        background: red;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        cursor: pointer;
        translate: 1s;
    }

    .counter__item-active {
        width: 50px;
        height: 20px;
        background: pink;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        translate: 1s;
        position: relative;
    }

    .count__progress {
        height: 100%;
        position: absolute;
        left: 0;
        background: rgba(255, 20, 10, .5);
    }
</style>
