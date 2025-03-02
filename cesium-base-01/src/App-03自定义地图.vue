<script setup>
import * as Cesium from 'cesium';
import { onMounted } from 'vue';
import { accessTokens } from "./constant/data.js";

let MAP_KEY = '89d42df20b98b129cecc8550b828a226';

onMounted(() => {

  Cesium.Ion.defaultAccessToken = accessTokens;

  // 设置默认视角
  Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
      89.6,  // 西边的经度
      20.4,  // 南边的纬度
      110.5, // 东边的经度
      61.2   // 北边的纬度
  );

  const viewer = new Cesium.Viewer('cesiumContainer', {
    geocoder: false,
    homeButton: false,
    sceneModePicker: false,
    baseLayerPicker: false,
    navigationHelpButton: false,
    animation: false,
    timeline: false,
    fullscreenButton: false,
    infoBox: true,
  });
  // 添加天地图影像图层
  // const imageryProvider = new Cesium.WebMapTileServiceImageryProvider({
  //   url: "http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=" + MAP_KEY,
  //   layer: "tdtVecBasicLayer",
  //   style: "default",
  //   format: "tiles",
  //   tileMatrixSetID: "GoogleMapsCompatible"
  // });
  // 添加天地图影像图层
  // viewer.imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
  //   url: "http://t0.tianditu.com/img_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=img&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=" + MAP_KEY,
  //   layer: "tdtBasicLayer",
  //   style: "default",
  //   format: "image/jpeg",
  //   tileMatrixSetID: "GoogleMapsCompatible"
  // }));
  // 添加openstreetmap影像图层
// 加载OSM在线地图（标准风格）
//   let imageryProvider= new Cesium.UrlTemplateImageryProvider({
//         url: 'https://tile-{s}.openstreetmap.fr/hot/{z}/{x}/{y}.png',
//         subdomains: ["a", "b", "c", "d"],
//       })
  //高德地图
  let imageryProvider = new Cesium.UrlTemplateImageryProvider({
    url: "http://webrd02.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}",
  });
  viewer.imageryLayers.addImageryProvider(imageryProvider);

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