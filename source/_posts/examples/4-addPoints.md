---
title: 添加点
type: examples
order: 4
---

### 添加点要素

{% raw %}
<button onclick="addPoint()">添加点</button>
<button onclick="addPoints()">添加多点</button>
<button onclick="removeClear()">清空</button>
<div id='map'></div>
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
Maps.initMap('map', {
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
      layerName: 'vector',
      isDefault: true,
      layerType: 'TileXYZ',
      opaque: false, //图层是否不透明
      layerUrl: 'http://171.34.40.68:6080/arcgis/rest/services/JXMAP_2016_2/MapServer',
    }
  ]
});
var points = [
  {
    attributes: {
      ID: '01',
      QLDM: 'Y236360922L0050',
      QLMC: '柏木桥',
      LXBM: 'Y236360922',
      LXMC: '赤兴至排江',
      QLZXZH: '7.4650000000',
      PYZH: '0.0000000000',
      QLQC: '23.0000000000',
      QMQK: '3.5000000000',
      ASYNXFLDM: '1.0000000000',
      XZQHBM: '360922'
    },
    geometry: 'POINT (115.92466595234826 27.428038204473552)',
    geometryType: 'Point'
  },
  {
    attributes: {
      ID: '02',
      QLDM: 'Y236360922L0050',
      QLMC: '柏木桥02',
      LXBM: 'Y236360922',
      LXMC: '赤兴至排江',
      QLZXZH: '7.4650000000',
      PYZH: '0.0000000000',
      QLQC: '23.0000000000',
      QMQK: '3.5000000000',
      ASYNXFLDM: '1.0000000000',
      XZQHBM: '360922'
    },
    geometry: 'POINT (115.79145292648322 27.62328784956489)',
    geometryType: 'Point'
  }
]
function addPoint () {
  Maps.addPoint(points[0], {
    layerName: 'test'
  });
}
function addPoints () {
  Maps.addPoints(points, {
    layerName: 'test'
  });
}
function removeClear () {
    Maps.removeFeatureByLayerName('test')
  }
</script>
{% endraw %}