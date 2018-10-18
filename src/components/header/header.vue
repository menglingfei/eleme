<template>
  <div class="header">
    <div class="main">
      <div class="avatar">
        <img width="100%" height="100%" :src="seller.avatar" />
      </div>
      <div class="content-wrap">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="transition">{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>
        <div v-if="seller.supports" class="activity">
          <div class="act-left">
            <span class="act-icon" :class="classMap[seller.supports[0].type]"></span>
            <span class="detail">{{seller.supports[0].description}}</span>
          </div>
        </div>
      </div>
      <div v-if="seller.supports" class="act-right" @click="showDetail">{{seller.supports.length}}个
        <i class="icon icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrap" @click="showDetail">
      <span class="bulletin-img"></span><span class="bulletin-content">{{seller.bulletin}}</span>
    </div>
    <div class="background">
      <img :src="seller.avatar" />
    </div>
    <div v-show="detailShow" class="detail-pop" transition="fade">
      <div class="detail-wrap clearfix">
        <div class="detail-title">{{seller.name}}</div>
        <div class="star-wrap">
          <star :score="seller.score" :size="48"></star>
        </div>
        <div class="divider-wrap">
          <div class="divider-line"></div>
          <div class="divider-content">优惠信息</div>
          <div class="divider-line"></div>
        </div>
        <ul class="coupon-wrap">
          <li :key="couponItem.id" v-for="couponItem in couponItems" class="coupon-items">
            <span class="coupon-icon" :class="classMap[couponItem.type]"></span>
            <span class="coupon-item-content">{{couponItem.description}}</span>
          </li>
        </ul>
        <div class="divider-wrap">
          <div class="divider-line"></div>
          <div class="divider-content">商家公告</div>
          <div class="divider-line"></div>
        </div>
        <div class="detail-content">{{seller.bulletin}}</div>
      </div>
      <div class="detail-close" @click="hideDetail">关闭</div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
    import star from '../star/star'
    export default {
      data () {
        return {
          detailShow: false
        }
      },
      name: 'header',
      props: {
        seller: {
          type: Object
        }
      },
      computed: {
        couponItems () {
          return this.seller.supports
        }
      },
      components: {
        star
      },
      created () {
        this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      },
      methods: {
        showDetail () {
          this.detailShow = true
        },
        hideDetail () {
          this.detailShow = false
        }
      }
    }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import '../../common/stylus/base.styl'
  @import '../../common/stylus/mixin.styl'
  // @import '../../common/stylus/icon.styl'
  .header
    position: relative
    color: #fff
    background-color: rgba(7, 17, 27, 0.5)
    overflow: hidden
    .background
      position: absolute
      left: 0
      top: 0
      bottom: 0
      right: 0
      z-index: -1
      filter: blur(10px)
      img
        width: 100%
        height: 100%
    .main
      display: flex
      position: relative
      padding: 24px 12px 18px 24px
      .avatar
        display: inline-block
        width: 64px
        height: 64px
        background-color: red
        img
          border-radius: 2px
      .content-wrap
        flex: 1
        display: inline-flex
        flex-direction: column
        margin-left: 16px
        color: rgb(255, 255, 255)
        .title
          margin-top: 2px
          font-size: 16px
          font-weight: bold
          line-height: 18px
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
        .transition
          margin-top: 8px
          font-size: 12px
          font-weight: 200px
          line-height: 12px
        .activity
          display: flex
          justify-content: space-between
          margin-top: 10px
          font-size: 10px
          font-weight: 200px
          line-height: 12px
          .act-left
            .act-icon
              display: inline-block
              width: 12px
              height: 12px
              margin-right: 4px
              background-size: 100% 100%
              background-repeat: no-repeat
              vertical-align: top
              &.decrease
                bg-image('decrease_1')
              &.guarantee
                bg-image('guarantee_1')
              &.discount
                bg-image('discount_1')
              &.invoice
                bg-image('invoice_1')
              &.special
                bg-image('special_1')
      .act-right
        position: absolute
        right: 12px
        bottom: 12px
        padding: 0 8px
        line-height: 24px
        border-radius: 14px
        font-size: 10px
        background-color: rgba(0, 0, 0, 0.2)
        .icon
          font-size: 10px
    .bulletin-wrap
      height: 28px
      line-height: 28px
      padding: 0 12px
      background-color: rgba(7, 17, 27, 0.2)
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      .bulletin-img
        display: inline-block
        width: 22px
        height: 12px
        margin-top: 8px
        bg-image('bulletin')
        background-size: 100% 100%
        background-repeat: no-repeat
        vertical-align: top
      .bulletin-content
        display: inline-block
        padding-left: 4px
        font-size: 10px
        vertical-align: top
    .detail-pop
      position: fixed
      top: 0
      left: 0
      width: 100%
      height: 100%
      background-color: rgba(7, 17, 27, 0.8)
      text-align: center
      z-index: 100
      overflow: auto
      transition: all 0.5s
      backdrop-filter: blur(10px)
      &.fade-transition
        opacity: 1
        background: rgba(7, 17, 27, 0.8)
      &.fade-enter, &.fade-leave
        opacity: 0
        background: rgba(7, 17, 27, 0)
      .detail-wrap
        width: 100%
        min-height: 100%
        .detail-title
          padding-top: 64px
          font-size: 16px
          font-weight: 700
          line-height: 16px
        .star-wrap
          margin-top: 16px
          line-height: 24px
        .divider-wrap
          display: flex
          margin: 28px 36px 24px 36px
          .divider-line
            flex: 1
            position: relative
            top: -8px
            border-bottom: 1px solid rgba(255, 255, 255, 0.2)
          .divider-content
            margin: 0 24px
            font-weight: 600
        .coupon-wrap
          padding: 0 36px
          .coupon-items
            list-style: none
            text-align: left
            margin: 0 12px 12px 12px
            font-size: 12px
            line-height: 12px
            .coupon-icon
              display: inline-block
              width: 16px
              height: 16px
              background-repeat: no-repeat
              background-size: 100% 100%
              vertical-align: top
              &.decrease
                bg-image('decrease_1')
              &.guarantee
                bg-image('guarantee_1')
              &.discount
                bg-image('discount_1')
              &.invoice
                bg-image('invoice_1')
              &.special
                bg-image('special_1')
            .coupon-item-content
              display: inline-block
              margin-left: 6px
              vertical-align: top
        .detail-content
          padding: 24px 48px 0 48px
          font-size: 12px
          line-height: 24px
          text-align: left
  .detail-close
    height: 64px
    margin-top: -64px
</style>
