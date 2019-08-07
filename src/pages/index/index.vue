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
      :previous-margin="previousMargin"
      :next-margin="nextMargin"
      @change="swiperChange" >
      <swiper-item v-for="(bannerItem, bannerIndex) in bannerList" :key="bannerIndex">
        <!-- 效果实现关键点，在于class名为image-container的元素的style中justify-content与padding的值，该值在currentIndex为0和最后一张图的时候，与其他位置的值不太一样，需要自行设定 -->
        <!-- padding值需要自己根据设计稿计算 -->
        <div class="image-container"
          :style="{
            justifyContent: currentIndex===0?((bannerIndex===bannerList.length-1)?'flex-end':(bannerIndex===1?'flex-start':'center')):(currentIndex===bannerList.length-1?(bannerIndex===0?'flex-start':(bannerIndex===bannerList.length-2?'flex-end':'center')):(bannerIndex===currentIndex-1?'flex-end':(bannerIndex===currentIndex+1?'flex-start':'center'))), 
            padding: currentIndex===0?((bannerIndex===bannerList.length-1)?'56rpx 26rpx 0 0':(bannerIndex===1?'56rpx 0 0 26rpx':'56rpx 0 0 0')):(currentIndex===bannerList.length-1?(bannerIndex===0?'56rpx 0 0 26rpx':(bannerIndex===bannerList.length-2?'56rpx 26rpx 0 0':'56rpx 0 0 0')):(bannerIndex===currentIndex-1?'56rpx 26rpx 0 0':(bannerIndex===currentIndex+1?'56rpx 0 0 26rpx':'56rpx 0 0 0')))
          }">
          <!-- 正在展示的图片放大一定倍数 -->
          <image class="slide-image" 
            :src="bannerItem" 
            :style="{
              transform: currentIndex===bannerIndex?'scale(' + scaleX + ',' + scaleY + ')':'scale(1,1)'
            }" 
            @click="getBannerDetail(bannerIndex)"/>
        </div>
      </swiper-item>
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
      previousMargin: '58rpx', // 前一张图片的外边距
      nextMargin: '58rpx', // 后一张图片的外边距
      currentIndex: 0,
      scaleX: 1.1527,
      scaleY: 1.1524,
      // 图片数组，需要至少3张图
      bannerList: [
        'https://mishi-image.oss-cn-hangzhou.aliyuncs.com/yry/wxapp/test/goodslist/menu-gulaorou.png',
        'https://mishi-image.oss-cn-hangzhou.aliyuncs.com/yry/wxapp/test/goodslist/menu-heniu.png',
        'https://mishi-image.oss-cn-hangzhou.aliyuncs.com/yry/wxapp/test/goodslist/menu-hongshaorou.png'
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
.image-container {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  display: flex;
}
.slide-image {
  width: 550rpx;
  height: 328rpx;
  z-index: 200;
  border-radius: 16rpx;
  transition-duration: .3s;
  transition-timing-function: 'ease';
}
</style>
