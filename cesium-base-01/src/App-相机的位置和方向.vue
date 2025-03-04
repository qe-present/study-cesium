<script setup>
import * as Cesium from 'cesium';
import { onMounted } from 'vue';
import { accessTokens } from "./constant/data.js";

let MAP_KEY = '89d42df20b98b129cecc8550b828a226';

onMounted(async () => {

  Cesium.Ion.defaultAccessToken = accessTokens;

  // 设置默认视角
  Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
      89.6,  // 西边的经度
      20.4,  // 南边的纬度
      110.5, // 东边的经度
      61.2   // 北边的纬度
  );

  const viewer = new Cesium.Viewer('cesiumContainer', {
    infoBox: false,
  });
  // setView 瞬间到达指定的位置
  // 天安门的位置
  let position = Cesium.Cartesian3.fromDegrees(116.39, 39.9, 1000)
  viewer.camera.setView({
    // 指定位置
    destination: position,
    //指定相机视角
    orientation: {
      heading: Cesium.Math.toRadians(0), // 水平方向 东南西北
      pitch: Cesium.Math.toRadians(-60), // 垂直方向 向上向下看
      roll: 0  // 侧倾角 转头
    }
  })



});
</script>

<template>
  <div id="cesiumContainer"></div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#cesiumContainer {
  width: 100%;
  height: 100vh;
}
</style>