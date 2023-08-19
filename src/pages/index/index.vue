<script setup lang="ts">
import type { BannerItem, CategoryItem, HotItem } from '@/types/home'
import CustomNavBar from './components/CustomNavBar.vue'
import { ref } from 'vue'
import { getHomeBannerAPI, getHomeCategoryAPI, getHomeHotAPI } from '@/services/home'
import { onLoad } from '@dcloudio/uni-app'
import CategoryPanel from './components/CategoryPanel.vue'
import HotPanel from './components/HotPanel.vue'

// 获取轮播图数据
const bannerList = ref<BannerItem[]>([])
const getHomeBannerData = async () => {
  const res = await getHomeBannerAPI()
  bannerList.value = res.result
}
// 获取前台分类数据
const categoryList = ref<CategoryItem[]>([])
const getHomeCategoryData = async () => {
  const res = await getHomeCategoryAPI()
  categoryList.value = res.result
}
// 获取热门推荐数据
const hotList = ref<HotItem[]>([])
const getHomeHotData = async () => {
  const res = await getHomeHotAPI()
  hotList.value = res.result
}

onLoad(async () => {
  await getHomeBannerData()
  await getHomeCategoryData()
  await getHomeHotData()
})
</script>

<template>
  <CustomNavBar />

  <XtxSwiper :list="bannerList" />

  <CategoryPanel :list="categoryList" />

  <HotPanel :list="hotList" />

  <view class="index"> </view>
</template>

<style lang="scss">
page {
  background-color: #f7f7f7;
}
</style>
