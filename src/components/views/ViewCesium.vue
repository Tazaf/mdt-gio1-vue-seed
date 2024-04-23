<template>
  <div id="param-cesium">
    <button type="button"  v-on:click="flytodirection(center,defaultheight,viewer);">Zoom sur le périmètre</button>
  </div>
  <div id="cesium-container"></div>
  <div id="toolbar"></div>
</template>

<script>
import 'cesium/Build/Cesium/Widgets/widgets.css';
import * as Cesium from 'cesium';


export default {
  name: 'CesiumGlobeView',
  data() {
    return {
      center: [6.412775, 46.550794],
      defaultheight: 3500,
      viewer: null
    };
  },
  methods: {
    /**
     * Fly to position
     *
     * @param {number[]} globecenter position to fly to
     * @param {number} globeheight altitude
     * @param {Viewer} viewer cesium viewer
     */
    flytodirection(globecenter, globeheight, viewer) {
      viewer.camera.flyTo({
        destination: Cesium.Cartesian3.fromDegrees(
          globecenter[0],
          globecenter[1],
          globeheight
        )
      });
    },
    /**
     * Init Cesium globe
     *
     * @returns {Viewer} viewer from cesium
     */
    setupCesiumGlobe() {
      let viewer = new Cesium.Viewer('cesium-container', {
        terrainProvider: new Cesium.createWorldTerrain(),
      });
      viewer.scene.primitives.add(Cesium.createOsmBuildings());
      return viewer;
    },
    addEntite(viewer,url) {
      viewer.entities.removeAll();
      let position = Cesium.Cartesian3.fromDegrees(
        6.412775,
        46.550794,
        750.0
      );
      let entity = viewer.entities.add({
        name: url,
        position: position,
        model: {
          uri: url,
        },
      });
      return entity
    },
  },
  mounted() {
    // add cesium ion token to the app
    // Cesium.Ion.defaultAccessToken = process.env.VUE_APP_CESIUM_ION_TOKEN;
    Cesium.Ion.defaultAccessToken = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwY2ZhOGUzOC1kYmQwLTRhMmQtODU2My0yNTkyYjBiYmRhZDkiLCJpZCI6MTE1MjMxLCJpYXQiOjE2Njg3MDQwNDF9.-B6cLmbix03DC71OJ22O-O7bT7_uHD05AejWRGwIhSk";
    
    this.viewer = this.setupCesiumGlobe();
    this.addEntite(this.viewer,'./GLTF_Writer.gltf');
    this.flytodirection(this.center, this.defaultheight, this.viewer);
  }
};
</script>

<style scoped>
#cesium-container {
  height: 500px;
}
</style>
