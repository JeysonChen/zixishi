<template>
  <view class="room-card" @tap="toDetail">
    <view class="room-card-logo">
      <image :src="`../../../${dataItem.logoUrl}`" mode="aspectFill"></image>
    </view>
    <view class="room-card-content">
      <view class="room-card-content-name">{{dataItem.studyRoomName}}</view>
      <view class="room-card-content-mark">{{dataItem.hotAnswerNum}}个热议问题</view>
      <view class="room-card-content-info">
          <u-tag text="热议" type="warning" size="mini" class="u-m-r-8"/>
          {{dataItem.hotAnswerCont}}
        </view>
    </view>
  </view>
</template>

<script>
export default {
  props: {
    dataItem: Object
  },
  methods: {
      toDetail() {
        uni.navigateTo({
            url: `/pages/forum/detail?id=${this.dataItem.id}`
        });
      }
  }
}
</script>

<style lang="scss">
.room-card {
    width: 100%;
  display: flex;
  background: #fff;
  margin-bottom: 20rpx;
  padding: 20rpx;
  box-sizing: border-box;
  overflow: hidden;
  border-radius: 20rpx;
  &-logo {
    width: 160rpx;
    height: 160rpx;
    margin-right: 20rpx;
    image {
        width: 160rpx;
        height: 160rpx;
        border-radius: 10rpx;
        
    }
  }
  &-content {
     flex: 1;
     
     width: 100%;
     overflow: hidden; 
    &-name {
        font-size: 32rpx;
        font-weight: bold;
        line-height: 60rpx;
    }
    &-mark {
        color: #999;
        line-height: 50rpx;
    }
    &-info {
        line-height: 50rpx;
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
        display: flex;
        align-items: center;
    }
  }
}
</style>