<template>
  <div
    v-if="show"
    :class="['full-image-wrapper', { 'zoom-in': zoomIn}]"
    @click="closeFullImage"
  >
    <div
      class="full-image"
      @click.stop="zoomInImage"
    >
      <img
        :src="img"
        alt="portfolio image"
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    img: {
      type: String,
      default: ''
    },
    show: {
      type: Boolean,
      default: false
    }
  },
  emits: ['update:show'],
  data() {
    return {
      zoomIn: false
    }
  },
  computed: {
    path() {
      return import.meta.env.BASE_URL
    }
  },
  created() {
    let that = this;
    document.addEventListener('keyup', function (evt) {
      if (evt.key === 'Escape') {
        that.closeFullImage();
      }
    });
  },
  methods: {
    closeFullImage() {
      this.$emit('update:show', false)
      document.body.classList.remove('overflow-hidden')
      this.zoomIn = false
    },
    zoomInImage(e) {
      this.zoomIn = !this.zoomIn
    }
  }
}
</script>

<style scoped lang="scss">
  .full-image-wrapper{
    position: fixed;
    top:0;left:0;right:0;bottom:0;
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(0,0,0,.85);
    padding: 30px;
    cursor: url('/x.png'), auto;
    .full-image{
      height: 100%;
      cursor: url('/plus.png'), auto;
      img{
        max-height: 100%;
      }
    }
    &.zoom-in{
      overflow: scroll;
      .full-image{
        cursor: url('/minus.png'), auto;	
        img{
          max-height: none;
        }
      }
    }
  }
</style>