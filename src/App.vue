<template>
  <div class="content">
    <TopSlider 
    :slides="items"
    :activeSlide = "activeSlide"
    :timer = "timer"
    @decrement="activeSlideDecrement"
    @increment="activeSlideIncrement"
    @setActive="setActiveSlide"
    />
  </div>
</template>

<script>
import TopSlider from "./components/TopSlider.vue"

export default {
  name: 'App',
  components: {
    TopSlider
  },

  data() {
    return {
      items: [
        {
          id: 1,
          img: "https://images.wallpaperscraft.ru/image/single/ulitsa_osveshchenie_podsvetka_134856_1920x1080.jpg",
          text: "Стич"
        },
        {
          id: 2,
          img: "https://img1.goodfon.ru/wallpaper/nbig/d/a2/full-hd-2560x1440-goroda.jpg",
          text: "хацкер"
        },
        {
          id: 3,
          img: "data:image/jpeg;base64,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",
          text: "Летательный аппарат"
        },
      ],
      activeSlide: 0,
      timer: 0
    }
  },

  methods: {
    activeSlideIncrement() {
      if (this.activeSlide >= this.items.length - 1) {
        this.activeSlide = 0
      } else {
        this.activeSlide++
      }
      this.timer = 0
    },

    activeSlideDecrement() {
      if (this.activeSlide == 0) {
        this.activeSlide = this.items.length - 1
      } else {
        this.activeSlide--
      }
      this.timer = 0
    },

    setActiveSlide(num) {
      this.activeSlide = num - 1
      this.timer = 0
    }
  },


  mounted() {
    setInterval(() => {
      if (this.timer !== 10000) {
        this.timer += 10
      } else {
        this.activeSlideIncrement()
        this.timer = 0
      }
    }, 1)
  },  

  watch: {
    activeSlide() {
      console.log("setActiveSlide")
    }
  }
  
}
</script>

<style>
#app {

}

.content {
  max-width: 1440px;
  padding: 20px;
  height: 100%;
  width: 100%;
  margin: 0 auto;
}
</style>
