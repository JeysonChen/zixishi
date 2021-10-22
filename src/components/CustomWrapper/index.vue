<template>
  <view class="custom-wrapper" :style="{minHeight: wrapperHeight}">
    <view class="status_bar">
      <!-- 这里是状态栏 -->
    </view>
    <view class="custom-wrapper-title" :style="{lineHeight: titleHeight, top: titleTop }">{{title}}</view>
    <view class="custom-wrapper-other" :style="{top: customHeight, height: otherHeight + 'px' }">
      <slot></slot>
    </view>
  </view>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: ''
    },
    otherHeight: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      customHeight: '',
      titleHeight: '',
      titleTop: '',
      wrapperHeight: ''
    }
  },
  mounted() {
    // 使用胶囊的位置来判断导航的位置
    console.log(uni.getMenuButtonBoundingClientRect(), 'uni.getMenuButtonBoundingClientRect()')
    let rect = uni.getMenuButtonBoundingClientRect()
    this.titleHeight = `${rect.height}px`
    this.customHeight = `${rect.bottom + 10}px`
    this.titleTop = `${rect.top}px`
    this.wrapperHeight = `${rect.bottom + this.otherHeight + 10}px`
    console.log(this.wrapperHeight, this.otherHeight, 'wroheiht')
  }
}
</script>

<style lang="scss">
.status_bar {
  height: var(--status-bar-height);
  width: 100%;
}
.custom-wrapper {
  position: relative;
  &-title {
    padding-left: 24rpx;
    position: absolute;
    font-size: 32rpx;
    font-weight: bold;
  }
  &-other {
    position: absolute;
    width: 100%;
    padding: 0 24rpx;
    box-sizing: border-box;
  }
}
</style>