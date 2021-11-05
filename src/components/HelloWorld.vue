<!--
 * @Descripttion: project
 * @Author: licheng
 * @Date: 2021-11-05 16:07:51
 * @LastEditors: licheng
 * @LastEditTime: 2021-11-05 16:55:34
-->
<template>
  <div class="View">
    <div id="cesiumContainer"></div>
  </div>
</template>

<script>
export default {
  name: "View",
  data() {
    return {
      token:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIyOTYzNWM0ZS1lZGJkLTRiNjktODRiOS0zZGJmZjYwZmMxMDUiLCJpZCI6NzI1MTAsImlhdCI6MTYzNjA5OTUwOH0.Yd5Hevb_48TCL2s4D7OF2c8iIJIAuwocjYo-O_CGcEo"
    };
  },
  mounted() {
    Cesium.Ion.defaultAccessToken = this.token;
    var viewer = new Cesium.Viewer("cesiumContainer", {
      animation: false,
      baseLayerPicker: false,
      fullscreenButton: false,
      vrButton: false,
      geocoder: false,
      homeButton: false,
      infoBox: false,
      sceneModePicker: false,
      selectionIndicator: false,
      timeline: false,
      navigationHelpButton: false,
      navigationInstructionsInitiallyVisible: false,
      imageryProvider: new Cesium.WebMapTileServiceImageryProvider({
        url:
          "http://t0.tianditu.com/img_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=img&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=594daef2db6509d78ea6d9601ce7ce4d",
        layer: "tdtImgBasicLayer",
        style: "default",
        format: "image/jpeg",
        show: false
      })
    });
    viewer.imageryLayers.addImageryProvider(
      new Cesium.WebMapTileServiceImageryProvider({
        url:
          "http://t0.tianditu.com/cia_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=cia&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=594daef2db6509d78ea6d9601ce7ce4d",
        layer: "tdtImgAnnoLayer",
        style: "default",
        format: "image/jpeg",
        tileMatrixSetID: "GoogleMapsCompatible",
        show: false
      })
    );
    viewer._cesiumWidget._creditContainer.style.display = "none";
    viewer.camera.flyTo({
      destination: Cesium.Cartesian3.fromDegrees(113.277178, 23.137995, 20000.0)
    });
  }
};
</script>

<style scoped>
#cesiumContainer {
  height: 100%;
}
</style>
