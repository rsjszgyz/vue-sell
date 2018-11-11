<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script>
import header from './components/header/header'
import { getSeller } from './api'
import qs from 'query-string'

export default {
  name: 'app',
  data() {
    return {
      seller: {
        id: qs.parse(location.search).id
      }
    }
  },
  components: {
    'v-header': header
  },
  created() {
    this._getSeller()
  },
  methods: {
    _getSeller() {
      getSeller({
        id: this.seller.id
      }).then((seller) => {
        this.seller = Object.assign({}, this.seller, seller)
      })
    }
  }
}
</script>

<style src="../static/css/reset.css"></style>

<style lang="stylus" rel="stylesheet/stylus">
@import './common/stylus/mixin.styl'
.tab
  display: flex
  width: 100%
  height: 40px
  line-height: 40px
  border-1px(rgba(7, 17, 27, 0.1))
  .tab-item
    flex: 1
    text-align: center
    & > a
      display: block
      font-size: 14px
      color: rgb(77, 85, 93)
      &.active
        color: rgb(240, 20, 20)
</style>


