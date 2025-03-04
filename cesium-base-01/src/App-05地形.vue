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
    // terrainProvider: await Cesium.createWorldTerrainAsync({ // 创建地形
    //   requestWaterMask: true, // 请求水面遮罩
    //   requestVertexNormals: true, // 请求顶点法线
    // })
    terrainProvider: new Cesium.CesiumTerrainProvider({
      url:"./terrain",
      requestWaterMask: true,
      requestVertexNormals: true
    })
  });


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