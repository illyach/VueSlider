<template>
  <div class="container">
    <div class="container2">
      <div ref="slider" class="images_container">
        <!-- Slider -->
        <!-- You can remove mounted if you dont want to autoplay -->
        <div
          class="action"
          :style="{ transform: `translateX(-${(activeSlide - 1) * 100.5}%)` }"
        >
          <!-- Item 1 -->
          <div class="images">
            <img
              src=".././assets/201.jpeg"
              alt=""
            />
          </div>
          <!-- Item 2 -->
          <div class="images">
            <img
              src=".././assets/202.jpeg"
              alt=""
            />
          </div>
          <!-- Item 3 -->
          <div class="images">
            <img
              src=".././assets/203.jpeg"
              alt=""
            />
          </div>

          <div class="images">
            <img
              src=".././assets/204.jpeg"
              alt=""
            />
          </div>
        </div>

        <!-- Prev/Next Arrows -->
        <div class="prev_next">
          <button @click="prevSlide" class="arrow-button">&#8592;</button>
          <button @click="nextSlide" class="arrow-button">&#8594;</button>
        </div>

        <!-- Dots Navigation -->
        <div class="dots">
          <button
            v-for="slideIndex in slideCount"
            :key="slideIndex"
            @click="activeSlide = slideIndex"
            :class="['dot-button', { 'active-dot': activeSlide === slideIndex }]"
          ></button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeSlide: 1,
      slideCount: 4,
      autoplayInterval: null,
    };
  },
  methods: {
    nextSlide() {
      this.activeSlide = this.activeSlide < this.slideCount ? this.activeSlide + 1 : 1;
    },
    prevSlide() {
      this.activeSlide = this.activeSlide > 1 ? this.activeSlide - 1 : this.slideCount;
    },
    startAutoplay() {
      this.autoplayInterval = setInterval(this.nextSlide, 5000); //5000
    },
    stopAutoplay() {
      clearInterval(this.autoplayInterval);
    },
  },
  mounted() { //когда компонент полностью загрузился
    this.startAutoplay();
  },
  beforeUnmount() { //до удаления
    this.stopAutoplay();
  },
};
</script>

<style scoped>

.images img{
width: 100%;
height: 100%;
object-fit: cover;
}


.container{
margin: 0 auto; 
width: 600px;
height: 800px;
}

.images_container{
  position: relative;
  overflow: hidden;
}


.action{
  transition: transform 500ms cubic-bezier(0.4, 0, 0.2, 1);
  /*transition: linear 0.3s;*/
  display: flex; /* Добавлено */
}
.images {
  flex: 0 0 100.5%; /* Изменено */
  box-sizing: border-box;
}

.prev_next{
display: flex; 
position: absolute; 
inset: 0 0 0 0; /*top right bottom left */
padding-left: 0.5rem;
padding-right: 0.5rem; 
justify-content: space-between; 
align-items: center; 
}

.dots{
    display: flex; 
    position: absolute; 
    right: 0; 
    bottom: 0; 
    left: 0; 
    padding: 1rem; 
    margin-left: 0.5rem; 
    justify-content: center; 
    gap:7px;
}

.arrow-button {
  width: 30px;
  height: 30px;
  background-color: rgba(0, 0, 0, 0.3);
  color: white;
  border: none;
  border-radius: 50%;
  cursor: pointer;
}

.dot-button {
  width: 12px;
  height: 12px;
  background-color: rgba(0, 0, 0, 0.3);
  border: none;
  border-radius: 50%;
  cursor: pointer;
}

.active-dot {
  background-color: #ff6600; /* Цвет активной точки */
}

/* Анимация слайдера */
@keyframes slide {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-200%);
  }
}

.animate-slider {
  animation: slide 5s linear infinite;
}
</style>


