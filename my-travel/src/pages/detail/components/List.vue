<template>
    <div>
      <div
        class="item"
        v-for="(item,index) of list"
        :key="index"
      >
        <div class="item-title border-bottom">
          <span class="item-title-icon"></span>
          <span>{{item.title}}</span>
        </div>
        <div v-if="item.children" class="item-children">
          <detail-list :list="item.children"></detail-list>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'DetailList',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
  .item-title
    line-height: .8rem
    font-size: .32rem
    padding: 0 .2rem
    .item-title-icon
      position: relative
      display: inline-block
      width: .36rem
      height: .36rem
      left: .06rem
      top: .06rem
      margin-right: .2rem
      background-size: .4rem .3rem
      background: url('http://s.qunarzz.com/piao/image/touch/sight/detail.png') 0 -0.45rem no-repeat
  .item-children
      padding: .2rem
</style>
