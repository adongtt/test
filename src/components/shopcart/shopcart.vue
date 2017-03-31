<template>
<div class="shopcart">
	<div class="content">
		<div class="content-left">
			<div class="logo-wrapper">
				<div class="logo" :class="{'highlight':totalCount>0}">
					<i class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></i>
				</div>
        <div class="num" v-show="totalCount > 0">{{totalCount}}</div>
			</div>
			<div class="price" :class="{'highlight':totalPrice>0}">
				￥{{totalPrice}}
			</div>
			<div class="desc">
				另需配送费￥{{deliveryPrice}}
			</div>
		</div>
		<div class="content-right">
			<div class="balance" :class="{'highlight':payClass===true}">
       {{payDesc}}
      </div>
		</div>
	</div>
</div>
</template>

<script>
export default{
  data: function () {
    return {total: 0}
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach((food) => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let total = 0
      this.selectFoods.forEach((food) => {
        total += food.count
      })
      return total
    },
    payDesc () {
      let diff = 0
      if (this.totalPrice === 0) {
        return `￥${this.minPrice}元起送`
      } else if (this.totalPrice < this.minPrice) {
        diff = this.minPrice - this.totalPrice
        return `还差￥${diff}元起送`
      } else {
        return `去结算`
      }
    },
    payClass () {
      if (this.totalPrice >= this.minPrice) {
        return true
      } else {
        return false
      }
    }
  },
  props: {
    selectFoods: {
      type: Array,
      default () {
        return []
      }
    },
    minPrice: {
      type: Number,
      default: 0
    },
    deliveryPrice: {
      type: Number,
      default: 0
    }
  }

}
</script>


<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/index'
.shopcart
  position: fixed
  left: 0
  bottom: 0
  width: 100%
  height: 48px
  .content
    display: flex
    background: #141D27
    font-size: 0
    .content-left
      flex: 1
      .logo-wrapper
        display: inline-block
        position: relative
        top: -10px
        margin: 0 12px
        padding: 6px
        width: 56px
        height: 56px
        box-sizing: border-box
        vertical-align: top
        border-radius: 50%
        background: #141D27
        .logo
          width: 100%
          height: 100%
          border-radius: 50%
          background: #2B343C
          text-align: center
          &.highlight
            background: #00A0DC
          .icon-shopping_cart
            font-size: 24px
            line-height: 44px
            color: #80858A
            &.highlight
              color: #fff
        .num
          position: absolute
          top: 0
          right: 0
          width: 24px
          height: 16px
          line-height: 16px
          border-radius: 6px
          font-size: 9px
          font-weight: 700
          color: rgb(255, 255, 255)
          text-align: center
          background: rgb(240, 20, 20)
          box-shadow: 0px 4px 8px 0px rgba(0, 0, 0, 0.4)
      .price
        display: inline-block        
        vertical-align: top
        line-height: 24px
        font-size: 16px
        font-weight: 700
        box-sizing: border-box
        padding-right: 12px
        color: rgba(255, 255, 255, 0.4)
        border-right: 1px solid rgba(255, 255, 255, 0.1)
        margin-top: 12px
        &.highlight
          color: #fff
      .desc
        display: inline-block
        vertical-align: top
        margin-top: 12px
        line-height: 24px
        font-size: 10px
        color: rgba(255, 255, 255, 0.4)
        padding: 0 12px
    .content-right
      flex: 0 0 105px
      width: 105px   
      background: #2B333B
      .balance
        height: 48px
        line-height: 48px
        text-align: center
        padding: 0 6px
        font-size: 12px
        font-weight: 200
        color: rgba(255, 255, 255, 0.4)
        &.highlight
          background: #00b43c
          color: #fff
</style>
