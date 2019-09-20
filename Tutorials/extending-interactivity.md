---
title: Extend with Mapbox.js
description: Meet Mapbox.js - the toolset for creating interactions and greater customization of your map and data.
thumbnail: extendingInteractivity
level: 2
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { geojsonSample } from '../../snippets/geojson-sample';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
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

本教程向你介绍怎样使用 [Mapbox.js](https://www.mapbox.com/mapbox.js/) ，一个渲染地图并能创建自定义交互的 JavaScript API。

{{
  <DemoIframe gl={false} src="/help/demos/extending-interactivity/index.html" />
}}

## 开始

本教程您需要准备：

* **你的 API 访问 token。** 如果您已经登录，我们自动将您的 token 添加到本教程中的示例中。 您可以在 [Account page](https://www.mapbox.com/account/) 找到您的 token 。
* **一个切片集 ID。** 您可以使用默认 Mapbox 样式中的 [tileset ID](/help/glossary/tileset-id) ，或者使用您自己 Mapbox Studio 经典项目中的。 您可以找到您项目中的切片集 ID 通过访问您的 [Classic projects page](https://www.mapbox.com/studio/classic/projects/)。本教程中未涉及到，但您可以按照 [these instructions](https://www.mapbox.com/studio-manual/overview/publish-your-style/#mapboxjs) 将您的 Mapbox Studio 样式添加到 Mapbox.js 地图中。
* **您最喜爱的文字编辑器**。您将编写一些 HTML 和 JavaScript 代码。

## 初始化一个地图

首先，您需要最新版本的 Mapbox.js 。你可以把这个片段复制到你的HTML文档中，直接链接到mapbox托管的版本:

```html
<script src='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.js'></script>
<link href='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.css' rel='stylesheet' />
```

为了在 Mapbox.js 中使用Mapbox 地图样式，您还需要一个 [style URL](/help/glossary/style-url/)。我们为您准备了一个占位符， `mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}`，但是您可以使用其它 [map style](https://docs.mapbox.com/api/maps/#styles)的样式 URL 将其替换，或者您可以用[Mapbox Studio](https://docs.mapbox.com/studio-manual/)创建自己自定义样式。

```html
<div id='map' class='map'> </div>
<script>
<script>
var map = L.mapbox.map('map')
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
</script>
```

### 坐标

现在您已经加载您的地图切片，设置初始位置和缩放级别，以便在加载页面时显示地图。您可以将 `setView` 添加到 `L.map()` 中，这样您的地图就可以打开到华盛顿特区。

```html
<div id='map' class='map'> </div>
<script>
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
</script>
```

### 禁用鼠标缩放

向下滚动具有地图的页面会导致不必要的滚动缩放。对于本教程，通过将 `scrollWheelZoom` 设置为 false 来禁用该交互。注意，您无法在地图上滚动缩放。

```html
<div id='map-three' class='map'> </div>
<script>
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  
</script>
```

## 添加数据

您可以向我们的地图添加数据，以帮助讲述一个故事、显示一个特性的位置或可视化一种趋势。 Mapbox.js 支持几种不同的格式，包括了 [GeoJSON](/help/glossary/geojson) ， [KML](/help/glossary/kml) ， 和 [CSV](/help/glossary/csv)。在这个样例中，您将从 GeoJSON 开始。

### GeoJSON

GeoJSON 是用于存储几何形状和标记位置的格式。下面是在GeoJSON中单个点的样子：

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.0366048812866,
          38.89784666877921
        ]
      },
      "properties": {}
    }
  ]
}
```

GeoJSON 看起来像象形文字吗？别担心。一旦你学会了这些模式，编写就会变得更容易。如果需要帮助，[geojson.net](http://geojson.net/) 为您编写和显示GeoJSON。

### 添加一个标记

将 GeoJSON 存储为一个名为 `geojson` 的变量，并创建一个 `featureLayer` 将其添加到地图中。

```javascript
var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
```

现在你有了地图上的标记：

```html
<div id='map' class='map'> </div>
<script>
var geojson = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-77.0366048812866, 38.89784666877921]
      },
      properties: {}
    }
  ]
};
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
</script>
```

如果您有很多地图元素，您可以将这些 GeoJSON 移动到一个文件中。您可以加载这些 GeoJSON 从 [by specifying its URL](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-url/)。您也可以从一个 [远程服务器比如GitHub](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-remote-url/) 加载一个文件。

### 自定义数据的样式

默认的灰色样式相当枯燥，但是您可以自定义它！您可以指定您自己的样式通过 GeoJSON 中的 `"properties": {}` 。这些样式是根据 [Simplestyle](https://github.com/mapbox/simplestyle-spec) 规则而定义的。 浏览 [specification](https://github.com/mapbox/simplestyle-spec/tree/master/1.1.0) 您可以了解更多关于所支持的属性名的信息。 

您还可以在属性对象中添加 `title` ，从而在这些地图元素上添加提示。

下面是添加了样式和标题的 GeoJSON 的样子：

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.0366048812866,
          38.89784666877921
        ]
      },
      "properties": {
        "title": "The White House",
        "marker-color": "#9c89cc",
        "marker-size": "medium",
        "marker-symbol": "building"
      }
    }
  ]
}
```

这是地图上定义样式的标记：

```html
<div id='map' class='map'> </div>
<script>
var geojson = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-77.0366048812866, 38.89784666877921]
      },
      properties: {
        title: 'The White House',
        'marker-color': '#9c89cc',
        'marker-size': 'medium',
        'marker-symbol': 'building'
      }
    }
  ]
};
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
</script>
```

单击标记查看提示！

### 添加一条线

通过添加 *其它* 标记并用一条线来连接它们，使您的地图更有趣一些

添加一个标记和线和它们的样式到我们已有的 GeoJSON 中。

```json
{{geojsonSample}}
```

下面是地图上您新定义了样式的地图元素：

```html
<div id='map' class='map'> </div>
<script>
var geojson = {{geojsonSample}};
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
</script>
```

## 添加一个图例

图例表述地图上的数据。 Mapbox.js 可以通过 `L.mapbox.legendControl.addLegend('Legend content')` 添加一个图例。`addLegend()` 方法使用 HTML Element 作为参数，所以请随意定制您的图例来满足您的需求！

默认情况下，图例出现在地图的右下角。但地图在一个狭小的空间里，当地图初始化时，通过设置 `position: 'topright'` 将图例放在上方。

图例现在出现在地图上：

```html
<div id='map' class='map'> </div>
<script>
var geojson = {{geojsonSample}};

var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);

L.mapbox.legendControl({ position: 'topright' }).addLegend('<strong>My walk from the White House to the hill!</strong>').addTo(map);
</script>
```

## 成品

你做到了！本教程涵盖了很多内容，我们希望您在离开的时候能够拥有创建自己的定制项目的技能和工具。

{{
  <DemoIframe gl={false} src="/help/demos/extending-interactivity/index.html" />
}}

## 下一个步骤

查看 [Mapbox.js examples](https://docs.mapbox.com/mapbox.js/examples/) 页面，了解更多的想法和代码，以帮助您进一步定制 Mapbox.js 项目。
