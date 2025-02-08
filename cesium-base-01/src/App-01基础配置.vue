<script setup>
import * as Cesium from 'cesium'
import { onMounted,ref } from 'vue'
import {accessTokens} from "./constant/data.js"

onMounted(() => {
  Cesium.Ion.defaultAccessToken = accessTokens
  // 设置默认视角
  Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
      // 西边的经度
      89.6,
      // 南边的纬度
      20.4,
      // 东边的经度
      110.5,
      // 北边的纬度
      61.2
  );
  const viewer = new Cesium.Viewer('cesiumContainer', {
    geocoder: true, // 是否显示位置查找工具（true表示是，false表示否）
    homeButton: true, // 是否显示首页位置工具
    sceneModePicker: true, //是否显示视角模式切换工具
    baseLayerPicker: true, //是杏显示默认图层选择工具
    navigationHelpButton: true, //是否显示导航帮助工具
    animation: true, //是杏显示动画工具
    timeline: true, //是否显示时间轴工具
    fullscreenButton: true, //是否显示全屏按钮工具
    infoBox: true, //是否显示信息框


  })
  viewer._cesiumWidget._creditContainer.style.display = 'none'
});
</script>

<template>
  <div id="cesiumContainer"></div>

</template>

<style scoped>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#cesiumContainer{
  width: 100%;
  height: 100vh;
}
</style>