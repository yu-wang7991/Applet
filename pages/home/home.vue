<template>
  <view>
    <swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
      <swiper-item v-for="(item,i) in swiperList" :key="i">
        <navigator class="swiper-item" :url="'/subpkg/good_detail/good_detail?good_id='+item.good_id">
          <img :src="item.image_src" alt="">
        </navigator>>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>
  export default {
    data() {
      return { swiperList: [], navList: [] }
    },
    onLoad() {
      this.getSwiperList()
      this.getNavList()
    },
    methods: {
      async getSwiperList() {
        const { data: res } = await uni.$http.get('/api/public/v1/home/swiperdata')
        if (res.meta.status !== 200) return uni.$showMsg()
        this.swiperList = res.message
      },
      async getNavList() {
        const { data: res } = await uni.$http.get('/api/public/v1/home/catitems')
        if (res.meta.status !== 200) return uni.$showMsg()
        this.navList = res.message
      }
    }
  }
</script>

<style lang="scss">
  .swiper-item {
    height: 330rpx;

    img {
      width: 100%;
      height: 100%;
    }
  }
</style>
