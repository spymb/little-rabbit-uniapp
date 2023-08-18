<script setup lang="ts">
import type { BannerItem } from '@/types/home'
import CustomNavBar from './components/CustomNavBar.vue'
import { ref } from 'vue'
import { getHomeBannerAPI } from '@/services/home'
import { onLoad } from '@dcloudio/uni-app'

// 获取轮播图数据
const bannerList = ref<BannerItem[]>([])
const getHomeBannerData = async () => {
  const res = await getHomeBannerAPI()
  bannerList.value = res.result
}

onLoad(async () => {
  await getHomeBannerData()
})
</script>

<template>
  <CustomNavBar />

  <XtxSwiper :list="bannerList" />

  <view class="index"> </view>
</template>

<style lang="scss">
//
</style>
