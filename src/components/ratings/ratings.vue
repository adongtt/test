<template>
<div class="ratings">
<div class="rating-wrapper">
<div class="left">
	<h1 class="score">{{seller.score}}</h1>
	<p class="text">综合评分</p>
	<span class="rankRate">高于周边商家{{seller.rankRate}}</span>
</div>
<div class="right">
<div class="score-wrapper">
<span class="title">服务态度</span>
<star :size="36" :score="seller.score" class="star"></star>
<span class="score">{{seller.serviceScore}}</span>
</div>
<div class="score-wrapper">
<span class="title">商品等级</span>
<star :size="36" :score="seller.foodScore" class="star"></star>
<span class="score">{{seller.foodScore}}</span>
</div>
<div class="score-wrapper">
<span class="title">送达时间</span>
<span class="time">{{seller.deliveryTime}}分钟</span>
</div>
</div>
</div>
<div class="main">
</div>
</div>
</template>

<script>
import star from '../star/star.vue'
const ERR_OK = 0
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data: function () {
    return {ratings: []}
  },
  mounted: function () {
    this.getRatings()
  },
  methods: {
    getRatings: function () {
      this.$http.get('/api/ratings').then(response => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.ratings = response.data
          console.log(this.ratings)
        }
      }, response => {
      })
    }
  },
  components: {
    star
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.ratings 
 position: absolute
 top: 174px
 bottom: 46px
 overflow: hidden 
 width: 100%
 .main 
   height: 24px
   background: #f3f5f7
   border-bottom: 1px solid #d9dde1
 .rating-wrapper
  display: flex
  top: 174px
  bottom: 46px
  overflow: hidden 
  width: 100%
  height: 106px
  border-bottom: 1px solid #d9dde1
  padding-top: 24px
  padding-bottom: 18px
  .left
   flex: 0 0 137.5px 
   width: 137.5px
   text-align: center
   border-right: 1px solid #d9dde1
   .score
     line-height: 28px
     font-size: 24px
     height: 28px
     color: rgb(255, 153, 0)
     margin-bottom: 6px
    .text
      line-height: 12px
      font-size: 12px
      color: rgb(7, 17, 27)
      margin-bottom: 8px
    .rankRate
      line-height: 10px
      font-size: 10px
      color: rgb(147, 153, 159)
      margin-bottom: 6px
  .right
   flex: 1
   padding: 0 24px
   .score-wrapper
     padding-bottom: 8px
     font-size: 0
     .title
       display: inline-block
       font-size: 12px
       line-height: 18px
       color: rgb(7, 17, 27)
       padding-right: 12px
       vertical-align: top
     .star 
       display: inline-block
       vertical-align: top
     .score
       display: inline-block
       vertical-align: top
       line-height: 18px
       font-size: 12px
       color: rgb(255, 153, 0)
      .time
        line-height: 18px
        font-size: 12px
        color: rgb(147, 153, 159) 
</style>
