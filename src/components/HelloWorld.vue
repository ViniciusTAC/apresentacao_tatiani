<template>
  <v-app style="background-color: #cdffbd">
    <v-container>
      <v-carousel
        v-model="currentSlide"
        :height="carouselHeight"
        hide-delimiters
        :show-arrows="false"
        class="custom-carousel"
      >
        <v-carousel-item
          v-for="(image, index) in images"
          :key="index"
        >
          <v-img
            :src="image.src"
            :alt="image.alt"
            contain
            class="carousel-image"
          ></v-img>
        </v-carousel-item>
      </v-carousel>

      <!-- Navigation buttons -->
      <div class="carousel-controls">
        <v-btn @click="prevSlide">Anterior</v-btn>
        <v-btn
          class="mx-2"
          v-for="(image, index) in images"
          :key="index"
          :class="{ 'active-button': currentSlide === index }"
          @click="goToSlide(index)"
        >
          {{ index + 1 }}
        </v-btn>
        <v-btn @click="nextSlide">Próximo</v-btn>
      </div>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      currentSlide: 0,
      images: [
        { src: require('@/assets/slide1.png'), alt: 'Slide 1' },
        { src: require('@/assets/slide2.png'), alt: 'Slide 2' },
        { src: require('@/assets/slide3.png'), alt: 'Slide 3' },
        { src: require('@/assets/slide4.png'), alt: 'Slide 4' },
        { src: require('@/assets/slide5.png'), alt: 'Slide 5' },
        { src: require('@/assets/slide6.png'), alt: 'Slide 6' },
        { src: require('@/assets/slide7.png'), alt: 'Slide 7' },
        { src: require('@/assets/slide8.png'), alt: 'Slide 8' },
      ],
    };
  },
  computed: {
    carouselHeight() {
      // Adjust height dynamically based on the screen size
      return window.innerWidth < 600 ? '50vh' : '90vh';
    },
  },
  methods: {
    prevSlide() {
      this.currentSlide =
        (this.currentSlide - 1 + this.images.length) % this.images.length;
    },
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.images.length;
    },
    goToSlide(index) {
      this.currentSlide = index;
    },
  },
};
</script>

<style>
html {
  scroll-behavior: smooth;
}

.carousel-image {
  height: 100%;
}

.caption {
  text-align: center;
  font-size: 16px;
  margin-top: 10px;
}

.carousel-controls {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 10px;
}

.carousel-controls v-btn {
  min-width: 40px;
  margin: 5px;
}

.active-button {
  background-color: #7fd664 !important;
  color: #fff !important;
}

/* Responsiveness */
@media (max-width: 600px) {
  .carousel-image {
    height: 50vh;
  }
  .carousel-controls {
    flex-direction: column;
    gap: 5px;
  }
}
</style>
