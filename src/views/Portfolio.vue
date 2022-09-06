<template>
  <div
    class="images-container images-container--large"
  >
    <div
      v-for="(image, i) in imagesLargeTop"
      :key="i"
      class="image-wrapper"
    >
      <img
        v-lazyload
        :data-url="image.pathLong"
        @click="displayFullImage(image)"
      >
    </div>
  </div>
  <div class="images-container images-container--small">
    <div
      v-for="(image, i) in imagesSmallMiddle"
      :key="i"
      class="image-wrapper"
    >
      <img
        v-lazyload
        :data-url="image.pathLong"
        @click="displayFullImage(image)"
      >
    </div>
  </div>
  <div class="images-container images-container--large">
    <div
      v-for="(image, i) in imagesLargeMiddle"
      :key="i"
      class="image-wrapper"
    >
      <img
        v-lazyload
        :data-url="image.pathLong"
        @click="displayFullImage(image)"
      >
    </div>
  </div>
  <div class="images-container images-container--small">
    <div
      v-for="(image, i) in imagesSmallBottomFirstHalf"
      :key="i"
      class="image-wrapper"
    >
      <img
        v-lazyload
        :data-url="image.pathLong"
        @click="displayFullImage(image)"
      >
    </div>
  </div>
  <div class="images-container images-container--small-secondary">
    <div
      v-for="(image, i) in imagesSmallBottomSecondHalf"
      :key="i"
      class="image-wrapper"
    >
      <img
        v-lazyload
        :data-url="image.pathLong"
        @click="displayFullImage(image)"
      >
    </div>
  </div>
  <FullImage
    v-model:show="showFullImage"
    :img="fullImagePath"
  />
</template>

<script>
import FullImage from '../components/FullImage.vue'

import lazyLoad from "../directives/lazyLoad.js";

export default {
  directives: {
    lazyload: lazyLoad
  },
  components: {
    FullImage
  },
  data() {
    return {
      images: [],
      showFullImage: false,
      fullImagePath: null
    }
  },
  computed: {
    imagesLargeTop () {
      return this.images.slice(0, 6)
    },
    imagesSmallMiddle () {
      return this.images.slice(6, 9)
    },
    imagesLargeMiddle () {
      return this.images.slice(9, 13)
    },
    imagesSmallBottomFirstHalf () {
      const n = this.images.length - 13
      const rest = Math.ceil(n / 2)%3
      const half = Math.ceil(n / 2) - rest
      return this.images.slice(-n).slice(0, half)
    },
    imagesSmallBottomSecondHalf () {
      const n = this.images.length - 13
      const rest = Math.ceil(n / 2)%3
      const half = Math.ceil(n / 2) - rest
      return this.images.slice(-n).slice(half)
    },
    isMobile () {
      return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)
    }
  },
  created(){
    this.importAll(import.meta.globEager("../assets/img/portfolio/*.jpg"))
  },
  methods: {
    importAll(r) {
      Object.keys(r).forEach(key => {
        this.images.push({ pathLong: r[key].default, pathShort: key })
      })
      this.images.sort((a, b) => {
        const aName = a.pathLong.replace(/^.*[\\\/]/, '')
        const bName = b.pathLong.replace(/^.*[\\\/]/, '')
        return aName.localeCompare(bName, 'en', { numeric: true })
      })
    },
    displayFullImage(image) {
      if (!this.isMobile) {
        this.showFullImage = true
        this.fullImagePath = image.pathLong
        document.body.classList.add('overflow-hidden')
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .images-container{
    display: grid;
    margin-right: -20px;
    @media (max-width: 960px) {
      margin-left: -10px;
    }
    @media (max-width: 500px) {
      display: block;
      margin-left: 0;
      margin-right: 0;
    }
    &--large{
      grid-template-columns: 4fr 5fr;
      .image-wrapper{
        padding: 30px 20px;
        margin-top: -30px;
        @media (max-width: 1200px) {
          padding: 20px 10px;
          margin-top: -20px;
        }
      }
    }
    &--small{
      grid-template-columns: 8fr 7fr 9fr;
      .image-wrapper{
        padding: 20px;
        margin-top: -20px;
        @media (max-width: 1200px) {
          padding: 10px;
          margin-top: -10px;
        }
      }
    }
    &--small-secondary{
      grid-template-columns: 7fr 9fr 8fr;
      .image-wrapper{
        padding: 20px;
        margin-top: -20px;
        @media (max-width: 1200px) {
          padding: 10px;
          margin-top: -10px;
        }
      }
    }
    .image-wrapper{
      display: flex;
      justify-content: center;
      align-items: center;
      @media (max-width: 500px) {
        padding: 0;
        margin-bottom: 15px;
        margin-top: 0;
      }
      img{
        max-width: 100%;
        cursor: pointer;
      }
    }
  }
  
</style>
