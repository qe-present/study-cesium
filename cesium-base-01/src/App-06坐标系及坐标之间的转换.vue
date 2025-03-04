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
    infoBox: true,
  });
  // 1 屏幕坐标系——二维坐标系 Cartesian2
  // 2 地理坐标系——WGS-84三维坐标系 Cartographic类型 经度、纬度、高度
  // 3 三维笛卡尔坐标系——Cartesian3类型

  // 角度转弧度
  let radius=Cesium.Math.toRadians(90)
  console.log(radius)
  // 弧度转角度
  let angle=Cesium.Math.toDegrees(radius)
  console.log(angle)
  // 经纬度转笛卡尔坐标
  let position = Cesium.Cartesian3.fromDegrees(116.39, 39.9, 1000)
  console.log(position)
  // 笛卡尔坐标转经纬度
  let cartographic = Cesium.Cartographic.fromCartesian(position)
  console.log(Cesium.Math.toDegrees(cartographic.longitude),Cesium.Math.toDegrees(cartographic.latitude),cartographic.height)
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