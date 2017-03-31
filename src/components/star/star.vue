<template>
<div class="star" :class="starType">
<span v-for="itemClass in itemClasses" :class="itemClass">
</span>
</div>
</template>

<script>
export default {
  props: {
    size: Number,
    score: Number
  },
  computed: {
    starType: function () {
      return 'star-' + this.size
    },
    itemClasses: function () {
      const LENGTH = 5
      const ON = 'on'
      const HALF = 'half'
      const OFF = 'off'
      let result = []
      let score = Math.floor(this.score * 2) / 2
      let integer = Math.floor(score)
      let hasDemical = score % 1 !== 0
      for (let i = 0; i < integer; i++) {
        result.push(ON)
      }
      if (hasDemical) {
        result.push(HALF)
      }

      while (result.length < LENGTH) {
        result.push(OFF)
      }
      return result
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/index'
.star
  &.star-48
    .on
      display: inline-block
      height: 20px
      width: 20px
      bg-image('star48_on')
      background-size: 20px 20px
      background-repeat: no repeat
      margin-right: 6px
    .half
      display: inline-block
      height: 20px
      width: 20px
      bg-image('star48_half')
      background-size: 20px 20px
      background-repeat: no repeat
      margin-right: 6px
    .off
      display: inline-block
      height: 20px
      width: 20px
      bg-image('star48_off')
      background-size: 20px 20px
      background-repeat: no repeat
      margin-right: 6px
    &:last-child
      margin-right: 0px
  &.star-36
    .on
      display: inline-block
      height: 16px
      width: 16px
      bg-image('star36_on')
      background-size: 16px 16px
      background-repeat: no repeat
      margin-right: 6px
    .half
      display: inline-block
      height: 16px
      width: 16px
      bg-image('star36_half')
      background-size: 16px 16px
      background-repeat: no repeat
      margin-right: 6px
    .off
      display: inline-block
      height: 16px
      width: 16px
      bg-image('star36_off')
      background-size: 16px 16px
      background-repeat: no repeat
      margin-right: 6px
    &:last-child
      margin-right: 0px
</style>
