<template>
<div class="goods">
<div class="menu-wrapper" ref="menuWrapper">
<ul class="menus">
<li v-for="(item,index) in goods" class="menu-item">
<span class="text">
<span v-show="item.type > 0" class="icon" :class="classMaps[item.type]"></span>{{item.name}}
</span>
</li>
</ul>
</div>
<div class="goods-wrapper" ref="goodsWrapper">
<ul>
  <li v-for="good in goods" class="food-list">
    <h1 class="title">{{good.name}}</h1>
    <ul>
    <li v-for="food in good.foods" class="food">
    <div class="icon">
      <img height="57" width="57" :src="food.icon" class="image">
    </div>
    <div class="content">
    <h2 class="name">{{food.name}}</h2>
    <p class="desc">{{food.description}}</p>
    <div class="extra">
      <span class="count">月售{{food.sellCount}}份</span>
      <span>好评率{{food.rating}}%</span>
    </div>
    <div class="price">
      <span class="newPrice">${{food.price}}</span><span v-show="food.oldPrice" class="oldPrice">${{food.oldPrice}}</span>
    </div>
    <div class="cartcontrol-wrapper">
      <cartcontrol :food="food"></cartcontrol>
    </div>
    </div>
    </li>
    </ul>
  </li>
</ul>
</div>
<shopcart :minPrice="seller.minPrice" :deliveryPrice="seller.deliveryPrice"></shopcart>
</div>
</template>

<script>
import BScroll from 'better-scroll'
import shopcart from '../shopcart/shopcart'
import cartcontrol from '../cartcontrol/cartcontrol.vue'
const ERR_OK = 0
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data: function () {
    return {goods: []}
  },
  created: function () {
    // console.log('created')
    this.classMaps = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      // return this.classMaps
      // console.log(this.classMaps)
    this.getGoods()
  },
  components: {
    shopcart,
    cartcontrol
  },
  methods: {
    getGoods: function () {
      this.$http.get('/api/goods').then(response => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.goods = response.data
          this.$nextTick(() => {
            this._initScroll()
          })
        }
      }, response => {
      })
    },
    _initScroll () {
      this.menuScroll = new BScroll(this.$refs.menuWrapper, { })
      this.goodScroll = new BScroll(this.$refs.goodsWrapper, {
        click: true,
        probeType: 3
      })
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/index'
.goods
 display: flex
 position: absolute
 top: 174px
 bottom: 46px
 overflow: hidden 
 width: 100%
 .menu-wrapper
  flex: 0 0 80px
  width: 80px
  background: #f3f5f7
  overflow-y: hidden
  .menu-item
   display: table
   height: 54px
   weight: 56px
   line-height: 14px
   padding: 0 12px
   .icon
    display: inline-block
    vertical-align: top
    width: 12px
    height: 12px
    margin-right: 4px
    background-size: 12px 12px
    background-repeat: no repeat
    &.decrease
     bg-image('decrease_3')
    &.discount
     bg-image('discount_3')
    &.special
     bg-image('special_3')
    &.invoice
     bg-image('invoice_3')
    &.guarantee
     bg-image('guarantee_3')
   .text
     display: table-cell
     width: 56px
     vertical-align: middle
     font-size: 12px
     font-weight: 200
 .goods-wrapper
   flex: 1
   .food-list
    .title
     height: 26px
     padding-left: 14px
     background: #f3f5f7
     line-height: 26px
     font-size: 12px
     color: rgb(147, 153, 159)
     border-left: 2px solid #d9dde1
    .food
      position: relative
      display: flex
      margin: 18px
      border-bottom: 1px solid #d9dde1
      padding-bottom: 18px
      &:last-child
        border-bottom: none
      .icon 
        flex: 0 0 57px
        margin-right: 10px
      .content 
        flex: 1
        .name
         line-height: 14px
         font-size: 14px
         color: rgb(7, 17, 27)
         padding-top: 2px
        .desc,.extra
         line-height: 12px
         font-size: 12px
         color: rgb(147, 153, 159)
         margin-top: 8px
         .extra 
           margin-right: 12px
        .price
          font-weight: 700
          line-height: 24px
          margin-top: 8px
          width: 52px
          .newPrice
            margin-right: 8px
            font-size: 14px
            color: rgb(240, 20, 20)
          .oldPrice
            font-size: 10px
            text-decoration: line-through
            color: rgb(147, 153, 159)            
        .cartcontrol-wrapper
          position: absolute
          right: 0
          bottom: 12px
          // z-index: 20
          // height: 48px
</style>
