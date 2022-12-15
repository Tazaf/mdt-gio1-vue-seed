<template>
  <div id="ol-container" class="map"></div>
</template>

<script>
import 'ol/ol.css';
import Map from 'ol/Map';
import WMTS from 'ol/source/WMTS';
import TileLayer from 'ol/layer/Tile';
import source from 'ol/source';
import tilegrid from 'ol/tilegrid/WMTS';
import * as olProj from 'ol/proj/';
import { register } from 'ol/proj/proj4';
import proj4 from 'proj4';
import View from "ol/View"

//Projection Suisse MN95
proj4.defs("EPSG:2056", "+proj=somerc +lat_0=46.95240555555556 +lon_0=7.439583333333333 +k_0=1 +x_0=2600000 +y_0=1200000 +ellps=bessel +towgs84=674.374,15.056,405.346,0,0,0,0 +units=m +no_defs");

register(proj4)

//Constante pour le WMST Cadastre
const resolutions = [
  4000, 3750, 3500, 3250, 3000, 2750, 2500, 2250, 2000, 1750, 1500, 1250,
  1000, 750, 650, 500, 250, 100, 50, 20, 10, 5, 2.5, 2, 1.5, 1, 0.5
];

const extent = [2420000, 130000, 2900000, 1350000];
const projection = olProj.get('EPSG:2056');
// console.log(projection)
projection.setExtent(extent);

const matrixIds = [];
for (var i = 0; i < resolutions.length; i++) {
  matrixIds.push(i);
}


//Création d'un WMTS cadastre vaud
const wmtsCadastre = new TileLayer({
  source: new WMTS(({
    layer: 'asitvd.fond_cadastral',
    crossOrigin: 'anonymous',
    url: '//wmts.asit-asso.ch/wmts/1.0.0/{Layer}/default/default/0/2056/{TileMatrix}/{TileRow}/{TileCol}.png',
    tileGrid: new tilegrid({
      origin: [extent[0], extent[3]],
      resolutions: resolutions,
      matrixIds: matrixIds
    }),
    requestEncoding: 'REST'
  })),
  visible: true
});

//Création des paramètres de vue (zoom et centre)
const view_map = new View({
  center: [2521400, 1156000],
  projection: projection,
  zoom: 12,
  maxZoom: 16
});


export default {

  mounted() {
    const map = new Map({
      target: "ol-container",
      view: view_map,

    });

    map.addLayer(wmtsCadastre);


  }
};
</script>

<style scoped>
#ol-container {
  height: calc(100% - 80px);
}
</style>
