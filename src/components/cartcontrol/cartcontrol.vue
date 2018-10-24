<template>
  <div class="cartcontrol">
    <span class="minus" v-show="food.count>0" @click="decreaseNum">-</span>
    <span class="count" v-show="food.count>0">{{food.count}}</span>
    <span class="plus" @click="addNum">+</span>
  </div>
</template>
<script type="text/ecmascript-6">
  import Vue from 'vue'
  export default {
    name: 'cartcontrol',
    props: {
      food: {
        type: Object
      }
    },
    computed: {
    },
    methods: {
      addNum () {
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1)
        } else {
          this.food.count++
        }
      },
      decreaseNum () {
        if (this.food.count) {
          this.food.count--
        }
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import '../../common/stylus/mixin.styl'
  .cartcontrol
    .minus
      display: inline-block
      width: 24px
      height: 24px
      line-height: 24px
      border-radius: 50%
      background-color: rgb(255, 255, 255)
      border: 2px solid rgb(0, 160, 220)
      box-sizing: border-box
      color: rgb(0, 160, 220)
      font-weight: 700
      vertical-align: top
      text-align: center
    .count
      display: inline-block
      width: 12px
      height: 24px
      line-height: 24px
      font-size: 10px
      color: rgb(147, 153, 159)
      text-align: center
      vertical-align: top
    .plus
      display: inline-block
      width: 24px
      height: 24px
      line-height: 24px
      border-radius: 50%
      background-color: rgb(0, 160, 220)
      color: #fff
      font-weight: 700
      vertical-align: top
      text-align: center
</style>
