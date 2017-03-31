<template>
<div class="cartcontrol">
  <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click="cartDecrease"></div>
  <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
  <div class="cart-add icon-add_circle" @click="cartAdd"></div>
</div>
</template>

<script>
import Vue from 'vue'
export default {
  props: {
    food: {
      type: Object
    }
  },
  created: function () {
  },
  methods: {
    cartDecrease () {
      if (!event._constructed) {
        return
      } else {
        if (this.food.count > 0) {
          this.food.count --
        }
        console.log(this.food.count)
      }
    },
    cartAdd () {
      if (!event._constructed) {
        return
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count ++
      }
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/index'
.cartcontrol
  font-size: 0
  .cart-decrease, .cart-add 
    display: inline-block
    height: 24px
    width: 24px
    padding: 6px
    line-height: 24px
    font-size: 24px
    color: rgb(0, 160, 220)
    vertical-align: top
  .cart-count 
    display: inline-block
    height: 36px
    line-height: 36px
    font-size: 10px
    color: rgb(147, 153, 159)
    padding: 0 4px
    vertical-align: top
</style>
