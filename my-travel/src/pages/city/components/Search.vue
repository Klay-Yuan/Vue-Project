<template>
    <div>
      <div class="search">
        <input type="text" placeholder="输入城市名或拼音" class="search-input" v-model="keyword">
      </div>
      <div class="search-content" ref="search" v-show="keyword">
        <ul>
          <li
          v-for="item of list"
          :key="item.id"
          class="search-item border-bottom"
          @click="handleCityClick(item.name)"
          >{{item.name}}</li>
          <li class="search-item border-bottom" v-show="hasNoData">
            没有找到匹配数据
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  computed: {
    hasNoData () {
      return !this.list.length
    }
  },
  methods: {
    handleCityClick (city) {
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.includes(this.keyword) || value.name.includes(this.keyword)) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/variables.styl'
  .search
    height: .72rem
    background: $bgColor
    padding: .1rem
    .search-input
      box-sizing: border-box
      padding: 0 .1rem
      height 0.62rem
      line-height: .62rem
      width: 100%
      text-align: center
      border-radius: .06rem
      color: #666
  .search-content
    overflow: hidden
    position: absolute
    top: 1.68rem
    z-index: 1
    left: 0
    bottom: 0
    right: 0
    background: #eeeeee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      color: #666
      background: #ffffff
</style>
