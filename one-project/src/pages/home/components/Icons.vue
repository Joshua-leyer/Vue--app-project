<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page, index) of pages" :key="index">
        <div
          class="icon"
          v-for="item of page"
          :key="item.id"
        >
          <div class='icon-img'>
            <img class='icon-img-content' :src='item.imgUrl' />
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return { //icons的自动滚动问题
      swiperOption: {
        autoplay: false
      }
    //   iconList: [{
    //         id: '001',
    //         imgUrl:'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
    //         desc: '酒店'
    //     }, {
    //         id: '002',
    //         imgUrl:'https://s.qunarzz.com/homenode/images/touchheader/flight.png',
    //         desc: '飞机'
    //     }, {
    //         id: '003',
    //         imgUrl:'https://s.qunarzz.com/homenode/images/touchheader/train.png',
    //         desc: '火车'
    //     }, {
    //         id: '004',
    //         imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/package.png',
    //         desc: '度假'
    //     }, {
    //         id: '005',
    //         imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/piao.png',
    //         desc: '景点门票'
    //     }, {
    //         id: '006',
    //         imgUrl: 'https://picbed.qunarzz.com/f5e5770393d759578962e53ee67798c8.png',
    //         desc: '海外酒店'
    //     }, {
    //         id: '007',
    //         imgUrl: 'https://picbed.qunarzz.com/ae617a31e0bd5803d76918b817f6d942.png',
    //         desc: '自由行'
    //     }, {
    //         id: '008',
    //         imgUrl: 'https://picbed.qunarzz.com/1316dc82d1ce6259686d5a68880e5a9d.png',
    //         desc: '攻略'
    //     }, {
    //         id: '009',
    //         imgUrl: 'https://picbed.qunarzz.com/377db8cb2143aebf01869c9baad3d325.png',
    //         desc: '汽车票船票'
    //     }
    //     ]
    }
  },
  computed: {
    pages () {
      const pages = []

      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~style/varibles.styl'
  @import '~style/mixins.styl'
  .icons >>> .swiper-container
    height: 0
    padding-bottom: 50%
  .icons
    margin-top: .1rem
    .icon
      position: relative
      overflow: hidden
      float: left
      width: 25%
      height: 0
      padding-bottom: 25%
      .icon-img
        position: absolute
        top: 0
        left: 0
        right: 0
        bottom: .44rem
        box-sizing: border-box
        padding: .1rem
        .icon-img-content
          display: block
          margin: 0 auto
          height: 100%
      .icon-desc
        position: absolute
        left: 0
        right: 0
        bottom: 0
        height: .44rem
        line-height: .44rem
        text-align: center
        color: $darkTextColor
        ellipsis()
</style>
