<template>
  <div id="app">
  <my-header :seller="seller"></my-header>
  <div class="tab">
    <div class="tab-item">
    <router-link to="/goods">商品</router-link>
  </div>
    <div class="tab-item">
    <router-link to="/ratings">评价</router-link>
    </div>
    <div class="tab-item">
    <router-link to="/seller">商家</router-link>
    </div>
  </div>
  <router-view :seller="seller"></router-view>
  </div>
  
</template>

<script>
import header from 'components/header/header.vue'
const ERR_OK = 0
export default {
  data: function () {
    return {seller: {}}
  },
  mounted: function () {
    this.getSeller()
  },
  components: {
    'my-header': header
  },
  methods: {
    getSeller: function () {
      this.$http.get('/api/seller').then(response => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.seller = response.data
        }
      }, response => {
      })
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import 'common/stylus/mixin'
#app
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
