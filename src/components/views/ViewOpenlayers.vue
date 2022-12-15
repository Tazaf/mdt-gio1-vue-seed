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
import GeoJSON from 'ol/format/GeoJSON';
import { Vector as VectorSource } from 'ol/source';
import { Circle as CircleStyle, Fill, Stroke, Style } from 'ol/style';
import { Vector as VectorLayer } from 'ol/layer';
import Feature from 'ol/Feature';
import Circle from 'ol/geom/Circle';

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

// LAYER de la carte
// ================================================================================
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

//LECTEUR DE DONNEES VECTORIEL
// ================================================================================

//CASIER
const casier = {
  "type": "FeatureCollection",
  "name": "casier",
  "features": [
    { "type": "Feature", "properties": {}, "geometry": { "type": "MultiLineString", "coordinates": [[[2521312.443, 1155801.203], [2521306.984999999869615, 1155807.982], [2521276.151, 1155845.638], [2521235.733, 1155887.605], [2521201.032000000122935, 1155920.862], [2521156.591, 1155950.928], [2521144.364, 1155957.712], [2521110.132000000216067, 1155961.356], [2521067.904999999795109, 1155965.27], [2521027.842999999877065, 1155969.489], [2520958.347, 1155971.302], [2520955.12099999981001, 1155973.504], [2520948.21, 1155981.752], [2520921.875, 1156016.207], [2520916.546999999787658, 1156023.439]]] } },
    { "type": "Feature", "properties": {}, "geometry": { "type": "MultiLineString", "coordinates": [[[2521016.974, 1156135.699], [2521226.969, 1156095.808999999891967], [2521495.072999999858439, 1155928.526]]] } },
    { "type": "Feature", "properties": {}, "geometry": { "type": "MultiLineString", "coordinates": [[[2521144.364, 1155957.712], [2521292.58600000012666, 1156205.504999999888241]]] } },
  ]
};
const casier_c = new VectorLayer({
  source: new VectorSource({
    features: new GeoJSON().readFeatures(casier),
  }),
  style: new Style({
    stroke: new Stroke({
      color: 'rgb(20, 0, 0, 1)',
      width: 2
    })
  }),
  visible: true
});

//PERIMETRE
const perimgeojson = {
  "type": "FeatureCollection",
  "name": "perimetre",
  "features": [
    { "type": "Feature", "properties": { }, "geometry": { "type": "MultiLineString", "coordinates": [ [ [ 2520485.26299999980256, 1156285.377 ], [ 2520487.177000000141561, 1156288.997 ], [ 2520489.904999999795109, 1156287.334 ], [ 2520487.867999999783933, 1156283.827 ], [ 2520485.26299999980256, 1156285.377 ] ] ] } },
    { "type": "Feature", "properties": { }, "geometry": { "type": "MultiLineString", "coordinates": [ [ [ 2521100.469, 1155797.449 ], [ 2521104.370000000111759, 1155803.3 ], [ 2521111.203000000212342, 1155814.038 ], [ 2521117.600999999791384, 1155826.834 ], [ 2521132.859000000171363, 1155838.571 ], [ 2521137.055000000167638, 1155838.571 ], [ 2521148.832, 1155836.216 ], [ 2521168.068, 1155819.602 ], [ 2521180.291000000201166, 1155833.571 ], [ 2521185.56, 1155833.571 ], [ 2521232.56, 1155833.571 ], [ 2521250.890999999828637, 1155833.571 ], [ 2521277.56900000013411, 1155840.847 ], [ 2521249.933000000193715, 1155809.96 ], [ 2521237.866, 1155776.543 ], [ 2521267.824, 1155771.984 ], [ 2521341.744, 1155820.392 ], [ 2521442.048, 1155886.077 ], [ 2521480.376000000163913, 1155911.177 ], [ 2521484.08, 1155913.92 ], [ 2521487.443, 1155917.07 ], [ 2521490.421999999787658, 1155920.587 ], [ 2521492.977, 1155924.422 ], [ 2521495.072999999858439, 1155928.526 ], [ 2521496.683999999891967, 1155932.844 ], [ 2521497.787, 1155937.319 ], [ 2521498.367999999783933, 1155941.891 ], [ 2521498.42, 1155946.499 ], [ 2521497.941000000108033, 1155951.082 ], [ 2521463.741, 1156160.673 ], [ 2521444.207, 1156163.074 ], [ 2521434.404, 1156164.895 ], [ 2521352.024000000208616, 1156188.446 ], [ 2521349.78899999987334, 1156188.923 ], [ 2521198.816000000108033, 1156232.686 ], [ 2521157.33, 1156247.476 ], [ 2521131.069999999832362, 1156266.95 ], [ 2521057.916999999899417, 1156171.774 ], [ 2521041.27, 1156154.069 ], [ 2521016.974, 1156135.699 ], [ 2520995.211999999824911, 1156149.773 ], [ 2520903.085, 1156001.821 ], [ 2520879.390000000130385, 1155830.965 ], [ 2521089.881, 1155799.057 ], [ 2521100.469, 1155797.449 ] ] ] } }
  ]
};
const perim = new VectorLayer({
  source: new VectorSource({
    features: new GeoJSON().readFeatures(perimgeojson),
  }),
  style: new Style({
    stroke: new Stroke({
      color: 'blue',
      lineDash: [10],
      width: 4
    })
  }),
  visible: true
});




//Création des paramètres de vue (zoom et centre)
// ================================================================================
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
    map.addLayer(casier_c);
    map.addLayer(perim);



  }
};
</script>

<style scoped>
#ol-container {
  height: calc(100% - 80px);
}
</style>
