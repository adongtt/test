<template>
<div class="header">
<div class="content-wrapper">
    <div class="avatar">
        <img class="img" width="64" height="64" :src="seller.avatar"></img>
    </div>
    <div class="content">
      <div class="title">
        <span class="brand"></span>
        <span class="name">{{seller.name}}</span>
      </div>
      <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达
      </div>
      <div v-if="seller.supports" class="support">
        <span class="icon" :class="classMaps[seller.supports[0].type]"></span>
        <span class="text">{{seller.supports[0].description}}</span>
      </div>
    </div>
    <div v-if="seller.supports" class="support-count">
      <span class="count" @click="showDetail">{{seller.supports.length}}个</span>
      <i class="icon-keyboard_arrow_right" ></i>
    </div>
</div>
<div class="bulletin-wrapper" @click="showDetail">
  <span class="bulletin-title"><img class="img"></img></span><span class="bulletin-text">{{seller.bulletin}}</span>
</div>
<div class="background"><img :src="seller.avatar" width="100%" height="100%"></img></div>
<transition name="fade">
<div v-show="detailShow" class="detail">
  <div class="detail-wrapper clearfix">
  <div class="detail-main">
    <h1 class="title">{{seller.name}}</h1>
     <div class="star-warpper">
  <star :score="seller.score" :size="48"></star>
  </div>
  <div class="benifit">
    <div class="line"></div>
    <div class="text">优惠信息</div>
    <div class="line"></div>
  </div>
  <ul v-if="seller.supports" class="supports">
    <li v-for="(item,index) in seller.supports" class="support-item">
     <span class="icon" :class="classMaps[seller.supports[index].type]"></span>
     <span class="text">{{seller.supports[index].description}}</span>
    </li>
  </ul>
  <div class="benifit">
    <div class="line"></div>
    <div class="text">商家信息</div>
    <div class="line"></div>
  </div>
  <div class="bulletin">
    <p class="content">{{seller.bulletin}}</p>
  </div>
  </div>

  </div>
  <div class="detail-close">
    <i class="icon-close" @click="closeDetail"></i>
  </div>
</div>
</transition>
</div>
</template>

<script>
import star from '../star/star.vue'
export default {
  data () {
    return {
      detailShow: false
    }
  },
  props: {
    seller: {
      type: Object
    }
  },
  created: function () {
    // console.log('created')
    this.classMaps = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      // return this.classMaps
      // console.log(this.classMaps)
  },
  methods: {
    showDetail () {
      this.detailShow = true
    },
    closeDetail () {
      this.detailShow = false
    }
  },
  components: {
    star
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/index'
.header
  position: relative
  color: #fff
  overflow: hidden
  background: rgba(7, 17, 27, 0.5)
  .content-wrapper
    position: relative
    padding: 24px 12px 18px 24px
    color: rgba(7,17,27,0.5)
    blur:10px
    font-size: 0
    .avatar
      display: inline-block
      .img
        border-radius: 2px
    .content
      display: inline-block
      margin-left: 16px
      font-size: 0px
      .title 
        margin: 2px 0 8px 0
        .brand
          display: inline-block
          width: 30px
          height: 18px
          bg-image('brand')
          background-size: 30px 18px
          background-repeat: no repeat
          vertical-align: top
          margin-right: 6px
        .name
          font-size: 16px
          font-weight: bold
          line-height: 18px
          color: rgb(255,255,255)
      .description
        margin-bottom: 10px
        line-height: 12px
        font-size: 12px
        font-weight: 200
        color: rgb(255,255,255)
      .support
        .icon
          display: inline-block
          vertical-align: top
          width: 12px
          height: 12px
          margin-right: 4px
          background-size: 12px 12px
          background-repeat: no repeat
          &.decrease
            bg-image('decrease_1')
          &.discount
            bg-image('discount_1')
          &.special
            bg-image('special_1')
          &.invoice
            bg-image('invoice_1')
          &.guarantee
            bg-image('guarantee_1')
        .text
          line-height: 12px
          font-size: 10px
          color: rgb(255,255,255)
    .support-count
      position: absolute
      right: 12px
      bottom: 18px
      padding: 0 8px
      height: 24px
      line-height: 24px
      border-radius: 14px
      background: rgba(0, 0, 0, 0.2)
      color: rgb(255,255,255) 
      .count
        vertical-align: top
        font-size: 10px
      .icon-keyboard_arrow_right
        font-size: 10px
        line-height: 24px
  .bulletin-wrapper
    height: 28px
    line-height: 28px
    padding: 0 22px 0 12px
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background-color: rgba(7, 17, 27, 0.2)
    .bulletin-title
      display: inline-block
      vertical-align:top
      width: 22px
      height: 12px
      margin-top: 8px
      background-size: 22px 12px
      background-repeat: no repeat
      bg-image('bulletin')
    .bulletin-text
      font-size: 10px
      margin-left: 4px
      margin-right: 2px
      vertical-align: top
      color: rgb(255, 255, 255)
  .background
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
    z-index: -1
    filter: blur(10px)
  .detail
    position: fixed
    top: 0
    left: 0
    z-index: 100
    width: 100%
    height: 100%
    overflow: auto
    background: rgba(7, 17, 27, 0.8)
    &.fade-enter-active,&.fade-leave-active
      transition: opacity .5s      
    &.fade-enter, &.fade-leave-active
      opacity: 0
    .detail-wrapper
      min-height: 100%
      width: 100%
      .detail-main
        margin-top: 64px
        padding-bottom: 64px
        .title
          line-height: 20px
          font-size: 20px
          font-weight: 700
          color: rgb(255, 255, 255)
          text-align: center
       .star-warpper
         text-align: center
         margin-top: 16px
         margin-bottom: 28px
       .benifit
         display: flex
         width: 80%
         margin: 28px auto 24px auto
         .line
           flex: 1
           position: relative
           top: -6px
           border-bottom: 1px solid rgba(255, 255, 255, 0.2)
         .text
           padding: 0 12px
           font-weight: 700
           font-size: 14px
       .supports
          width: 80%
          margin: 0 auto
         .support-item
           margin-bottom: 12px
           .icon
            display: inline-block
            width: 16px
            height: 16px
            margin-right: 6px
            background-size: 16px 16px
            background-repeat: no repeat
            vertical-align: top
            &.decrease
             bg-image('decrease_2')
            &.discount
             bg-image('discount_2')
            &.special
             bg-image('special_2')
            &.invoice
             bg-image('invoice_2')
            &.guarantee
             bg-image('guarantee_2')
            .text
             line-height: 12px
             font-size: 12px
             font-weight: 200
             color: rgb(255,255,255)
       .bulletin
         width: 80%
         margin: 0 auto
         padding-left: 12px
         padding-right: 12px
         .content
           font-size: 12px
           line-height: 24px
           font-weight: 200
           color: rgb(255, 255, 255)
    .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        .icon-close
          font-size: 32px
          color: rgba(255, 255, 255, 0.5)
</style>
