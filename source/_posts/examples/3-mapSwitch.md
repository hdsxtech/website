---
title: 底图切换
type: examples
order: 3
---

### 底图切换
  
{% raw %}
  <button onclick="changeLayer('vector')">基本地图</button>
  <button onclick="changeLayer('earth')">影像地图</button>
  <button onclick="changeLayer('panorama')">地形图</button>
  <div id='switchMap'></div>
 <script>
 var cor = [
     {
       "level": 0,
       "resolution": 0.010986328383069278,
       "scale": 4617150
     },
     {
       "level": 1,
       "resolution": 0.005493164191534639,
       "scale": 2308575
     },
     {
       "level": 2,
       "resolution": 0.0027465809060368165,
       "scale": 1154287
     },
     {
       "level": 3,
       "resolution": 0.0013732916427489112,
       "scale": 577144
     },
     {
       "level": 4,
       "resolution": 6.866458213744556E-4,
       "scale": 288572
     },
     {
       "level": 5,
       "resolution": 3.433229106872278E-4,
       "scale": 144286
     },
     {
       "level": 6,
       "resolution": 1.716614553436139E-4,
       "scale": 72143
     },
     {
       "level": 7,
       "resolution": 8.582953794130404E-5,
       "scale": 36071
     },
     {
       "level": 8,
       "resolution": 4.291595870115493E-5,
       "scale": 18036
     },
     {
       "level": 9,
       "resolution": 2.1457979350577466E-5,
       "scale": 9018
     },
     {
       "level": 10,
       "resolution": 1.0728989675288733E-5,
       "scale": 4509
     },
     {
       "level": 11,
       "resolution": 5.363305107141452E-6,
       "scale": 2254
     },
     {
       "level": 12,
       "resolution": 2.681652553570726E-6,
       "scale": 1127
     }
   ];
   var resolutions = [];
   for (var i = 0; i < cor.length; i++) {
     resolutions.push(cor[i].resolution);
   }
   var Maps = new HMap.Map();
   Maps.initMap('switchMap', {
     interactions: {
       altShiftDragRotate: true,
       doubleClickZoom: true,
       keyboard: true,
       mouseWheelZoom: true,
       shiftDragZoom: true,
       dragPan: true,
       pinchRotate: true,
       pinchZoom: true,
       zoomDelta: 1, // 缩放增量（默认一级）
       zoomDuration: 500 // 缩放持续时间
     },
     controls: {
       attribution: true,
       attributionOptions: {
         className: 'ol-attribution', // Default
         target: 'attributionTarget',
       },
       rotate: true,
       rotateOptions: {
         className: 'ol-rotate', // Default
         target: 'rotateTarget',
       },
       zoom: true,
       zoomOptions: {
         className: 'ol-zoom', // Default
         target: 'zoomTarget',
       },
       overViewMapVisible: false,
       scaleLineVisible: true
     },
     view: {
       center: [115.92466595234826, 27.428038204473552],
       resolutions: resolutions,
       fullExtent: [109.72859368643232, 24.010266905347684, 121.13105988819079, 30.76693489432357],
       tileSize: 256,
       origin: [-400, 399.9999999999998],
       enableRotation: true, // 是否允许旋转
       projection: 'EPSG:4326',
       rotation: 0,
       zoom: 1, // resolution
       zoomFactor: 2 // 用于约束分变率的缩放因子（高分辨率设备需要注意）
     },
     logo: {},
     baseLayers: [  // 不传时默认加载OSM地图。
       {
         layerName: 'vector', // 图层名，必传
         isDefault: false, // 是否是默认图层
         layerType: 'TileXYZ', // 图层类型（arcgis加载的为TileXYZ）
         layerUrl: 'http://171.34.40.68:6080/arcgis/rest/services/JXMAP_2016_2/MapServer',
       },
       {
         layerName: 'earth',
         layerType: 'TitleWMTS',
         layer: 'img',
         isDefault: false,
         layerUrl: 'http://t{0-6}.tianditu.cn/img_c/wmts',
         label: { // 对应的标注层
           layerName: 'TDTLabel',
           layerType: 'TitleWMTS',
           layer: 'cia',
           alias: 'earth', // 标注层所关联的图层
           isDefault: false,
           layerUrl: 'http://t{0-6}.tianditu.cn/cia_c/wmts'
         }
       },
       {
         layerName: 'panorama',
         layerType: 'TitleWMTS',
         layer: 'ter',
         isDefault: true,
         layerUrl: 'http://t{0-6}.tianditu.com/ter_c/wmts',
         label: {
           layerName: 'TDTLabel',
           layerType: 'TitleWMTS',
           layer: 'cia',
           alias: 'panorama',
           isDefault: false,
           layerUrl: 'http://t{0-6}.tianditu.cn/cia_c/wmts'
         }
       }
     ]
   });
   var layerSwitcher = new HMap.LayerSwitcher(Maps.map);
   function changeLayer (type) {
     // type 对应的baseLayers图层组的layerName
     layerSwitcher.switchLayer(type)
   }
   </script>
{% endraw %}
