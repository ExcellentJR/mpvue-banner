<template>
  <div class="banner-container">
    <swiper :style="{width: '100vw', height: '410rpx'}" 
      :indicator-dots="indicatorDots" 
      :indicator-color="indicatorColor" 
      :indicator-active-color="indicatorActiveColor"
      :autoplay="autoplay" 
      :interval="interval" 
      :duration="duration" 
      :circular="circular"
      @change="swiperChange" 
      :previous-margin="'58rpx'"
      :next-margin="'58rpx'">
      <div 
        v-for="(bannerItem, bannerIndex) in bannerList" 
        :key="bannerIndex">
        <swiper-item>
          <div 
            :style="{
              boxSizing: 'border-box', 
              width: '100%', 
              height: '100%', 
              display: 'flex', 
              justifyContent: currentIndex===0?((bannerIndex===bannerList.length-1)?'flex-end':(bannerIndex===1?'flex-start':'center')):(currentIndex===bannerList.length-1?(bannerIndex===0?'flex-start':(bannerIndex===bannerList.length-2?'flex-end':'center')):(bannerIndex===currentIndex-1?'flex-end':(bannerIndex===currentIndex+1?'flex-start':'center'))), 
              padding: currentIndex===0?((bannerIndex===bannerList.length-1)?'56rpx 26rpx 0 0':(bannerIndex===1?'56rpx 0 0 26rpx':'56rpx 0 0 0')):(currentIndex===bannerList.length-1?(bannerIndex===0?'56rpx 0 0 26rpx':(bannerIndex===bannerList.length-2?'56rpx 26rpx 0 0':'56rpx 0 0 0')):(bannerIndex===currentIndex-1?'56rpx 26rpx 0 0':(bannerIndex===currentIndex+1?'56rpx 0 0 26rpx':'56rpx 0 0 0')))
            }">
            <image :src="bannerItem" 
              class="slide-image" 
              :style="{
                transform: currentIndex===bannerIndex?'scale(' + scaleX + ',' + scaleY + ')':'scale(1,1)',
                transitionDuration: '.3s',
                transitionTimingFunction: 'ease'
              }" 
              @click="getBannerDetail(bannerIndex)"/>
          </div>
        </swiper-item>
      </div>
    </swiper>
  </div>
</template>

<script>

export default {
  data () {
    return {
      indicatorDots: true,
      indicatorColor: 'rgba(255, 255, 255, .4)',
      indicatorActiveColor: 'rgba(255, 255, 255, 1)',
      autoplay: false,
      interval: 3000,
      duration: 300,
      circular: true,
      currentIndex: 0,
      animationIndex: 0,
      scaleX: 1.1527,
      scaleY: 1.1524,
      bannerList: [
        'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
        'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg',
        'http://img06.tooopen.com/images/20160818/tooopen_sy_175833047715.jpg'
      ]
    }
  },
  methods: {
    swiperChange (e) {
      this.currentIndex = e.mp.detail.current
      this.scaleX = 1.1527
      this.scaleY = 1.1524
    },
    getBannerDetail (index) {
      console.log(index)
      wx.showToast({
        title: '可加上跳转链接',
        icon: 'none'
      })
    }
  }
}
</script>

<style scoped>
.banner-container {
  width: 100vw;
  height: 524rpx;
}
.slide-image {
  width: 550rpx;
  height: 328rpx;
  z-index: 200;
  border-radius: 16rpx;
}
</style>
