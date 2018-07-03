<template>
  <div>
    <div class="search">
      <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音" />
    </div>
    <ul class="list" v-if="keyword">
      <li
       class="item border-bottom"
       v-for="item in list"
       :key="item.id"
       v-if="list.length"
      >{{item.name}}
      </li>
      <li class="item border-bottom">没有找到匹配数据</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: []
    }
  },
  mounted () {
    console.log('初始值:' + this.list.length)
  },
  watch: {
    keyword () {
      const result = []
      for (let i in this.cities) {
        this.cities[i].forEach((val) => {
          if (this.keyword && (val.spell.indexOf(this.keyword) > -1 ||
            val.name.indexOf(this.keyword) > -1)) {
            result.push(val)
          }
        })
      }
      this.list = result
      console.log(this.list.length)
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .search
    height:.72rem
    padding:0 .1rem
    background: $bgColor
    .search-input
      width:100%
      height:.62rem
      line-height:.62rem
      padding:0 .1rem
      box-sizing:border-box
      color:#666
      border-radius:.06rem
  .list
    position:absolute
    top:1.58rem
    left:0
    right:0
    bottom:0
    background:#eee
    z-index:10
    .item
      padding-left:.2rem
      line-height:.76rem
      background:#fff
</style>
