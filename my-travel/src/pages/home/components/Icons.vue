<template>
    <div class="icons">
      <swiper :options="swiperOption">
        <swiper-slide v-for="(page, index) of pages" :key="index">
            <div class="icon" v-for="item of page" :key="item.id">
                <div class="icon-img">
                <img class="icon-img-content" :src="item.imgURL" >
                <p class="icon-desc">{{item.title}}</p>
                </div>
            </div>
        </swiper-slide>
      </swiper>
    </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/variables.styl'
@import '~styles/mixins.styl'
  .icons >>> .swiper-container
    height: 0
    padding-bottom: 50%
  .icons
    margin-top: .2rem
    .icon
      overflow:hidden
      float: left
      width: 25%
      height: 0
      padding-bottom: 25%
      position: relative
      .icon-img
        position: absolute
        top: 0
        left: 0
        right: 0
        bottom: .44rem
        .icon-img-content
          height: 100%
          margin:0 auto
          display: block
        .icon-desc
          position: absolute
          bottom: -.4rem
          left: 0
          right: 0
          height: .44rem
          line-height: .44rem
          color: $dartTextColor
          text-align: center
          min-width: 0
          ellipsis()
</style>
