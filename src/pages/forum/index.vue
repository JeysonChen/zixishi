<template>
  <view class="wrapper">
    <view class="forum-custom-wrapper wrapper-header">
      <custom-wrapper title="自习室" :otherHeight="otherHeight">
        <view style="width: 100%">
          <u-search placeholder="请输入关键词" :show-action="false" bg-color="#fff" v-model="keyword"></u-search>
        </view>
      </custom-wrapper>
    </view>
    <view class="wrapper-body">
      <view class="u-tabs-box">
        <u-tabs-swiper
          activeColor="#f29100"
          ref="tabs"
          :list="tabList"
          :current="current"
          @change="change"
          :is-scroll="false"
          swiperWidth="750"
        ></u-tabs-swiper>
      </view>
      <swiper class="swiper-box u-padding-24" :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish">
        <swiper-item class="swiper-item" v-for="(list, i) in tabList" :key="i">
          <scroll-view scroll-y style="height: 100%;" @scrolltolower="reachBottom">
            <view class="page-box">
              <view v-if="i==0" ><image src="../../static/images/ad/1.png" style="width: 100%; height: 160rpx; border-radius: 20rpx;" mode=""></image></view>
              <view class="u-flex u-row-center"  v-if="loading">
                <u-loading mode="circle"></u-loading>
              </view>
              <view v-else>
                <view v-if="i==0">
                  <u-dropdown active-color="#f29100">
                    <u-dropdown-item v-model="orderBy" title="综合排序" :options="orderList"></u-dropdown-item>
                  </u-dropdown>
                </view>
                <room-card v-for="(item, index) in dataList[i]" :key="index" :dataItem="item" />
              </view>
            </view>
          </scroll-view>
        </swiper-item>
      </swiper>
    </view>
  </view>
</template>

<script>
import CustomWrapper from '../../components/CustomWrapper'
import RoomCard from './modules/RoomCard.vue'
import { tabList, orderList } from './config'
import { getStudyRoomList, getCaredStudyRoomList, getRecommendStudyRoomList, getOtherStudyRoomList } from './data'
export default {
  onShow() {},
  data() {
    return {
      otherHeight: 44,
      tabList,
      current: 0,
      swiperCurrent: 0,
      tabsHeight: 0,
      dx: 0,
      loadStatus: ['loadmore', 'loadmore', 'loadmore', 'loadmore'],
      dataList: [],
      loading: false,
      orderBy: '1', // 综合排序
      orderList,
    }
  },
  components: {
    CustomWrapper,
    RoomCard
  },
  mounted() {
    this.getList(0)
  },
  watch: {
    orderBy(val, oldVal) {
      if (val && val != oldVal) {
        this.getList(0);
      }
    }
  },
  methods: {
    reachBottom() {
      console.log('reachBottom')
    },
    getList(index) {
      this.loading = true
      setTimeout(() => {
        this.loading = false
        this.dataList = []
        switch (index) {
          case 0:
            this.dataList[0] = getStudyRoomList()
            break
          case 1:
            this.dataList[1] = getCaredStudyRoomList()
            break
          case 2:
            this.dataList[2] = getRecommendStudyRoomList()
            break
          case 3:
            this.dataList[3] = getOtherStudyRoomList()
            break
        }
        this.loadStatus.splice(index, 1, 'loadmore')
      }, 700)
    },

    // tab栏切换
    change(index) {
      this.swiperCurrent = index
      this.getList(index)
      // this.getOrderList(index)
    },
    transition({ detail: { dx } }) {
      this.$refs.tabs.setDx(dx)
    },
    animationfinish({ detail: { current } }) {
      this.$refs.tabs.setFinishCurrent(current)
      this.swiperCurrent = current
      this.current = current
      this.getList(current)
    }
  }
}
</script>

<style lang="scss">
.wrapper {
  height: 100vh;
  display: flex;
  flex-direction: column;
  &-body {
    flex: 1;
    background: #f9f9f9;
    overflow: auto;
    display: flex;
    flex-direction: column;

    .swiper-box {
      flex: 1;
    }
  }
  .page-box {
    .u-dropdown__menu__item  {
      justify-content: flex-start;
    }
  }
}
.forum-custom-wrapper {
  background: #fbbd08;
  // height: 200rpx;
}
</style>