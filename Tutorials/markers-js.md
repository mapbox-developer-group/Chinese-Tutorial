---
title: Work with markers in Mapbox.js
description: Add custom, interactive markers to your map with Mapbox.js.
thumbnail: markersJs
level: 2
topics:
- web apps
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { DemoStatic } from '../../components/demo-static';"
contentType: tutorial
language:
- JavaScript
---

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Add custom markers in Mapbox GL JS',
      link: '/help/tutorials/custom-markers-gl-js/'
    }}
  />
}}


在这份指南中，我们会展示给你如何添加 [markers](/help/glossary/marker/)，自定义标记并使它们与 Mapbox.js 交互。将这份指南作为你探索 Mapbox.js 中标记功能所有可能的指导吧！

## 准备开始

这份教程中，你需要用到 **your API access token** 你可以在你的 [Account page](https://www.mapbox.com/account/) 里找到它。为了更好地理解每个例子，你可以将全部源代码复制到本地项目和实验中。我们会在 [Mapbox.js examples](https://www.mapbox.com/mapbox.js/example/v1.0.0/) 中展示优秀应用。

## 添加标记

你可以通过 [Leaflet](http://leafletjs.com/) 或者使用 Mapbox.js 以 GeoJSON 格式向地图中添加标记。

### 在Leaflet中添加标记

你可以用 [L.marker](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-marker/) 在你的地图中添加 DOM 标记。在下面这个例子中，我们在地图中添加了已知坐标的标记。如果你只有少数标记需要添加，请使用这种方式。

```html
<div id='map-leaflet' class='map'> </div>
<script>
var mapLeaflet = L.mapbox.map('map-leaflet')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

L.marker([38.913184, -77.031952]).addTo(mapLeaflet);
L.marker([37.775408, -122.413682]).addTo(mapLeaflet);

mapLeaflet.scrollWheelZoom.disable();
</script>
```

### 在Mapbox.js使用GeoJSON格式添加标记

你也可以将标记的坐标存储为 [GeoJSON](/help/glossary/geojson/)，之后将 GeoJSON 加载并显示在你的地图文件中。在这个例子中，我们在 GeoJSON 文件中添加了并显示了 Mapbox 在华盛顿特区和旧金山的办公室位置。即使是处理较大的数据文件，GeoJSON中数据特征管理也是有序的。

```html
<div id='map_geo' class='map'> </div>
<script>
var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    }
  }
];

var mapGeo = L.mapbox.map('map_geo')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

var myLayer = L.mapbox.featureLayer().setGeoJSON(geojson).addTo(mapGeo);
mapGeo.scrollWheelZoom.disable();
</script>
```
你同样可以将 GeoJSON 作为外部文件 [hosted locally](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-url/)或在 [GitHub](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-remote-url/) 上加载。 在下一部分中，你会学到如何使用 [simplestyle specification](/help/glossary/simplestyle/) 对 GeoJSON 标记设置样式。

如果你刚刚开始使用 GeoJSON 文件，这里有一些可以帮助你生成、验证 GeoJSON 或者调整 GeoJSON 格式的工具：

- [geojson.net](https://geojson.net) &mdash; 生成和自定义 GeoJSON
- [`geojsonhint`](https://github.com/mapbox/geojsonhint) &mdash; 使用 Lint 工具验证 GeoJSON 
- [toGeoJSON](http://mapbox.github.io/togeojson/) &mdash; 将 KML 或 GPX 文件转换成 GeoJSON
- [csv2geojson](http://mapbox.github.io/csv2geojson/) &mdash; 将 CSV 文件转换成 GeoJSON

## 样式化标记

你可以向 GeoJSON 中加载 [simplestyle](/help/glossary/simplestyle/) 来实现样式化标记。你可以加载自定义图像，或者用 HTML 和 CSS 创造你自己的标记。    

### 使用 simplestyle 来样式化标记  

[Simplestyle spec](/help/glossary/simplestyle) 是一种针对 GeoJSON 的样式化标记。这意味着你可以向每个标记添加特定的关键词和值来改变标记的颜色、符号和大小。

以下是所有可用的样式化选项键值对：

键             | 值                     | 例子
------------------|------------------------|----------------
`"marker-color"`  | Any hex value<br>Example: `"#3bb2d0"` |  {{ <DemoStatic src="https://api.mapbox.com/v4/mapbox.light/pin-m+3bb2d0(-73.975,40.767)/auto/80x100@2x.png?access_token=MapboxAccessToken" alt="Blue-colored marker" width="80" /> }}
`"marker-symbol"` | Any [Maki icon name](https://labs.mapbox.com/maki-icons), an integer, or a lowercase letter<br> Example: `"1"` | {{ <DemoStatic src="https://api.mapbox.com/v4/mapbox.light/pin-m-1+3bb2d0(-73.975,40.767)/auto/80x100@2x.png?access_token=MapboxAccessToken" alt="marker with '1' symbol" width="80" /> }}
`"marker-size"`   | small, medium, large<br>Example: `"large"` | {{ <DemoStatic src="https://api.mapbox.com/v4/mapbox.light/pin-l-1+3bb2d0(-73.975,40.767)/auto/80x100@2x.png?access_token=MapboxAccessToken" alt="large marker" width="80" /> }}


在这个例子中，我们使用了 [GeoJSON from the previous section](#add-markers-with-geojson-in-mapboxjs) 并且向其添加了 simplestyle。 读者可以浏览源文件来看样式化标记是如何被添加到各个特性中的。

```html
<div id='map_simple' class='map'> </div>
<script>
var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  }
];

var mapSimple = L.mapbox.map('map_simple')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().setGeoJSON(geojson).addTo(mapSimple);
mapSimple.scrollWheelZoom.disable();
</script>
```

### 使用图片样式化标记

You can define a custom marker image in your GeoJSON by adding an `icon` object to each feature's `properties`. In this example, [L.icon](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-icon/) is used to set the marker image to each feature's `iconURL`.

你可以在 GeoJSON 中使用自定义标记图片向每个特征的 `properties` 添加 `icon`。 在下文例子中，我们将使用 [L.icon](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-icon/) 用于将标记图像设置为每个特性的 `iconURL`。

```html
<div id='map-one' class='map'> </div>
<script>
var mapOne = L.mapbox.map('map-one')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().addTo(mapOne);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut1.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut2.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  }
];
myLayer.on('layeradd', function(e) {
  var marker = e.layer,
    feature = marker.feature;
  marker.setIcon(L.icon(feature.properties.icon));
});
myLayer.setGeoJSON(geojson);
mapOne.scrollWheelZoom.disable();
</script>
```

### 使用 HTML 和 CSS 样式化标记

如果你想创建更高级的样式化标记，你可以用 `<div>` 来替换标准标记定义，并分配一个类给它，然后使用 CSS 中的 [L.divIcon](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-divicon/) 函数来实现个性化。在下文中，你会看到一个与 [marker image](#style-markers-with-an-image) 相似的例子，但这一次，我们会向各个特征分配一个类名称，然后将 CSS 添加到样式表中。

```html
<style>
.my-icon {
  border-radius: 100%;
  width: 20px;
  height: 20px;
  text-align: center;
  line-height: 20px;
  color: white;
}

.icon-dc {
  background: #3bb2d0;
}

.icon-sf {
  background: #3bb2d0;
}
</style>
<div id='map-two' class='map'> </div>
<script>
var mapTwo = L.mapbox.map('map-two')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

var myLayer = L.mapbox.featureLayer().addTo(mapTwo);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      icon: {
        className: 'my-icon icon-dc', // class name to style
        html: '&#9733;', // add content inside the marker, in this case a star
        iconSize: null // size of icon, use null to set the size in CSS
      }
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      icon: {
        className: 'my-icon icon-sf', // class name to style
        html: '&#9733;', // add content inside the marker, in this case a star
        iconSize: null // size of icon, use null to set the size in CSS
      }
    }
  }
];
myLayer.on('layeradd', function(e) {
  var marker = e.layer,
    feature = marker.feature;
  marker.setIcon(L.divIcon(feature.properties.icon));
});
myLayer.setGeoJSON(geojson);

mapTwo.scrollWheelZoom.disable();
</script>
```html

## Add popups

You can add popups with simplestyle in your GeoJSON or with JavaScript.

### Add popups with simplestyle

Simplestyle allows you to add popups automatically if you add `title` and `description` keys to each feature's properties. In the example below, these fields are added to the GeoJSON. Click the markers to trigger the popup.  

```html
<div id='map-popups' class='map'> </div>
<script>
var mapPopups = L.mapbox.map('map-popups')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().addTo(mapPopups);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      title: 'Mapbox DC',
      description: '1714 14th St NW, Washington DC',
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      title: 'Mapbox SF',
      description: '155 9th St, San Francisco',
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  }
];
myLayer.setGeoJSON(geojson);
mapPopups.scrollWheelZoom.disable();
</script>
```
通过在 GeoJSON 中添加 `title` 和 `description` 值，你可以向你的弹出窗口添加更多HTML元素（如链接、图片、视频、表单等等）。

### 通过JavaScript添加弹出窗口

你可以通过 [L.bindPopup](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-popup/) 函数来自定义每个弹出窗口的内容。在下文例子中，每个特征的属性中都添加了 `image` 关键词，然而，只有当 `bindPopup()` 函数被调用的时候，弹出窗口中才会出现图片。

```html
<div id='map-popups-js' class='map'> </div>
<script>
var mapPopupsJS = L.mapbox.map('map-popups-js')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().addTo(mapPopupsJS);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      title: 'Mapbox DC',
      description: '1714 14th St NW, Washington DC',
      image: 'https://farm9.staticflickr.com/8604/15769066303_3e4dcce464_n.jpg',
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut1.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      title: 'Mapbox SF',
      description: '155 9th St, San Francisco',
      image: 'https://farm9.staticflickr.com/8571/15844010757_63b093d527_n.jpg',
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut2.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  }
];

// Set a custom icon on each marker based on feature properties.
myLayer.on('layeradd', function(e) {
  var marker = e.layer,
    feature = marker.feature;
  marker.setIcon(L.icon(feature.properties.icon));
  var content = '<p><strong>' + feature.properties.title + '</strong></p><img src="' + feature.properties.image + '" alt="">';
  marker.bindPopup(content);
});
myLayer.setGeoJSON(geojson);
mapPopupsJS.scrollWheelZoom.disable();
</script>
```

### 更多例子

你可以通过 Mapbox.js 对你的弹出窗口进行更多自定义更改。如下例子可供参考：

* [向弹出窗口中添加图集](https://www.mapbox.com/mapbox.js/example/v1.0.0/markers-with-image-slideshow/)
* [展示标记之外的弹出窗口](https://www.mapbox.com/mapbox.js/example/v1.0.0/marker-tooltips-outside-map/)
* [在弹出窗口中添加视频](https://www.mapbox.com/mapbox.js/example/v1.0.0/video/)
* [在弹出窗口中添加音频片段](https://www.mapbox.com/mapbox.js/example/v1.0.0/soundcloud-embed/)
* [弹出窗口中的多个标签页](https://www.mapbox.com/mapbox.js/example/v1.0.0/marker-tooltip-tab-groups/)
* [使用CSS编辑弹出窗口格式](https://www.mapbox.com/mapbox.js/example/v1.0.0/custom-popup-style/)

## 标记聚类
  
当数据过于稠密时，你可以使用 Leaflet 的 Markercluster 插件来对你的数据进行可视化更改。如下的例子里，我们加载了外部 GeoJSON 文件，根据其中数据创建了 `clustergroup`，随后将它加入地图中。由于 Markercluster 是一个插件，你需要添加 [additional CSS and JS](https://www.mapbox.com/mapbox.js/plugins/#leaflet-markercluster) 来启用它。

```html
<script src='https://api.mapbox.com/mapbox.js/plugins/leaflet-markercluster/{{constants.VERSION_MAPBOXJS}}/leaflet.markercluster.js'></script>
<link href='https://api.mapbox.com/mapbox.js/plugins/leaflet-markercluster/{{constants.VERSION_MAPBOXJS}}/MarkerCluster.css' rel='stylesheet' />
<link href='https://api.mapbox.com/mapbox.js/plugins/leaflet-markercluster/{{constants.VERSION_MAPBOXJS}}/MarkerCluster.Default.css' rel='stylesheet' />
<div id='map-cluster' class='map'></div>
<script>
var mapCluster = L.mapbox.map('map-cluster')
  .setView([38.9, -77], 11)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
L.mapbox.featureLayer()
  .loadURL('/help/data/stations.geojson')
  .on('ready', function(e) {
    var clusterGroup = new L.MarkerClusterGroup();
    e.target.eachLayer(function(layer) {
      clusterGroup.addLayer(layer);
    });
    mapCluster.addLayer(clusterGroup);
  });
mapCluster.scrollWheelZoom.disable();
</script>
```

### 更多例子

你可以通过 Mapbox.js 对你的弹出窗口进行更多自定义更改。如下例子可以供读者参考：

* [使用 Mapbox 数据创建标记聚类](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-with-mapbox-data/)
* [多种不同风格的样式聚类](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-multiple-groups/)
* [自定义多边形风格的聚类](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-custom-polygon-appearance/)
* [自定义聚类图标的聚类](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-custom-marker-icons/)

## 切换图层

最后，让我们一起了解一下在 Mapbox.js 中如何切换图层。开发者可以帮助用户通过添加过滤条件，来筛选开启和关闭图层。在下文例子中，脚本自动为每条运输路线创建了切换选项，即只有在这条 `line` 在 GeoJSON 中被声明后，新图层才会被添加到切换列表中。

```html
<style>
.filter-ui {
  background: #fff;
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 100;
  padding: 10px;
  border-radius: 3px;
}

.filter-ui input {
  vertical-align: middle;
}
</style>
<nav id='filters' class='filter-ui'></nav>
<div id='map-toggle' class='map'></div>
<script>

var mapToggle = L.mapbox.map('map-toggle')
  .setView([38.9, -77], 11)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

var filters = document.getElementById('filters');

var markers = L.mapbox.featureLayer().loadURL('/help/data/examples/stations.geojson');

markers.on('ready', function(e) {
  var typesObj = {},
    types = [];
  var features = e.target._geojson.features;
  for (var i = 0; i < features.length; i++) {
    typesObj[features[i].properties.line] = true;
  }
  for (var key in typesObj) {
    if ({}.hasOwnProperty.call(typesObj, key)) {
      types.push(key);
    }
  }
  var checkboxes = [];
  for (var j = 0; j < types.length; j++) {
    var item = filters.appendChild(document.createElement('div'));
    var checkbox = item.appendChild(document.createElement('input'));
    var label = item.appendChild(document.createElement('label'));
    checkbox.type = 'checkbox';
    checkbox.id = types[j];
    checkbox.checked = true;
    label.innerHTML = types[j];
    label.setAttribute('for', types[j]);
    checkbox.addEventListener('change', update);
    checkboxes.push(checkbox);
  }

  function update() {
    var enabled = {};
    for (var k = 0; k < checkboxes.length; k++) {
      if (checkboxes[k].checked) enabled[checkboxes[k].id] = true;
    }
    markers.setFilter(function(feature) {
      return feature.properties.line in enabled;
    });
  }
}).addTo(mapToggle);
mapToggle.scrollWheelZoom.disable();
</script>
```

### 更多例子

读者可以研究如下例子来获得更多关于如何筛选或者切换你的标记的灵感：

- [通过标记符号筛选](https://www.mapbox.com/mapbox.js/example/v1.0.0/multiple-marker-filters/)
- [标记的多个过滤器](https://www.mapbox.com/mapbox.js/example/v1.0.0/markers-with-multiple-filters/)
- [切换图层](https://www.mapbox.com/mapbox.js/example/v1.0.0/layers/)

## 下一步

你现在有了向你的地图添加标记的工具、代码和灵感。你可以探索 [Build a store locator](/help/tutorials/building-a-store-locator-js/)这一教程来了解更多的方法来拓展你的 Mapbox.js 项目。
