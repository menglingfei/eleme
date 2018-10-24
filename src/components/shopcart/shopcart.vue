<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrap">
          <span class="logo" :class="totalCount > 0 ? 'highlight':''"></span>
          <span class="num" v-show="totalCount>0">{{totalCount}}</span>
        </div>
        <div class="price">￥{{totalPrice}}元</div>
        <div class="desc">另需配送费￥{{deliverPrice}}元</div>
      </div>
      <!--右侧有三种状态，1-什么都没买；2-买了但是不超过起送费；买了且超过了起送费-->
      <div class="content-right">
        <div class="pay" :class="totalPrice >= minPrice ? 'enough':'not-enough'">{{payDesc}}</div>
      </div>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
  export default {
    name: 'shopcart',
    props: {
      selectFoods: {
        type: Array
      },
      minPrice: {
        type: Number,
        default: 0
      },
      deliverPrice: {
        type: Number,
        default: 0
      }
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
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })
        return count
      },
      payDesc () {
        if (this.totalPrice === 0) {
          return `￥${this.minPrice}元起送`
        } else if (this.totalPrice > 0 && this.totalPrice < this.minPrice) {
          let diff = this.minPrice - this.totalPrice
          return `还差${diff}元`
        } else {
          return '去结算'
        }
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import '../../common/stylus/mixin.styl'
  .shopcart
    position: fixed
    left: 0
    bottom: 0
    z-index: 100
    width: 100%
    height: 48px
    .content
      display: flex
      height: 100%
      background-color: #141d27
      color: rgba(255, 255, 255, 0.4)
      .content-left
        flex: 1
        position: relative
        font-size: 0
        .logo-wrap
          position: absolute
          display: inline-block
          width: 56px
          height: 56px
          border-radius: 50%
          left: 12px
          bottom: 2px
          background-color: #141d27
          .logo
            position: absolute
            display: inline-block
            background-color: rgba(255, 255, 255, 0.4)
            width: 40px
            height: 40px
            border-radius: 50%
            left: 8px
            bottom: 8px
            z-index: 1000
            &.highlight
              background-color: rgb(0, 160, 220)
          .num
            position: absolute
            right: 0
            top: 0
            width: 24px
            height: 16px
            line-height: 16px
            text-align: center
            border-radius: 8px
            background-color: rgb(240, 20, 20)
            font-size: 9px
            font-weight: 700
            color: #fff
            box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
            z-index: 10000
        .price
          display: inline-block
          margin: 12px 0 12px 74px
          padding-right: 12px
          font-size: 16px
          font-weight: 700
          line-height: 24px
          border-right: 1px solid rgba(255, 255, 255, 0.4)
          color: #fff
        .desc
          display: inline-block
          margin-left: 12px
          font-size: 12px
          line-height: 24px
          font-weight: 500
      .content-right
        width: 105px
        font-size: 0
        .pay
          height: 48px
          line-height: 48px
          text-align: center
          font-size: 12px
          font-weight: 700px
          background-color: #2b333b
          &.not-enough
            background: #2b333b
          &.enough
            background: #00b43c
            color: #fff
</style>
