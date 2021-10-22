<template>
  <view class="wrap">
    <view>
      <u-swiper :list="swiperList" height="380"></u-swiper>
    </view>
    <view class="room-detail">
      <view class="room-detail-head u-flex">
        <view style="width: 100rpx; " class="room-detail-head-logo">
          <image src="../../static/images/logo/3.png" alt srcset />
        </view>
        <view class="u-flex-1">
          <view>渡夏冬虫自习室（明光桥店）</view>
          <view>2544个热议问题</view>
        </view>
        <view>
          <u-button type="primary" shape="circle" size="mini">关注</u-button>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      swiperList: [
        {
          image: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
          title: '昨夜星辰昨夜风，画楼西畔桂堂东'
        },
        {
          image: 'https://cdn.uviewui.com/uview/swiper/2.jpg',
          title: '身无彩凤双飞翼，心有灵犀一点通'
        },
        {
          image: 'https://cdn.uviewui.com/uview/swiper/3.jpg',
          title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
.room-detail {
  width: 100%;
  margin-top: -60rpx;
  background: #fff;
  position: relative;
  z-index: 99;
  border-radius: 30rpx;
  padding: 24rpx;

  &-head {
    &-logo {
      image {
        width: 160rpx;
        height: 160rpx;
      }
    }
  }
}
</style>