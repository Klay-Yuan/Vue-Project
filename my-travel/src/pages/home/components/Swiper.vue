<template>
  <div class="wrapper">
    <swiper :options="swiperOption" v-if="showSwiper">
        <swiper-slide v-for="item of list" :key="item.id">
            <img class="swiper-image" :src="item" />
        </swiper-slide>
        <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
    }
  }
}
</script>
<style lang="stylus" scoped>
  .wrapper >>> .swiper-pagination-bullet-active
    background: #fff
  .wrapper
    .swiper-image
      width: 100%
</style>
