---
title: Find elevations with the Tilequery API
description: Use the Mapbox Tilequery API and the Mapbox Terrain tileset to create an app that returns the elevation at a specified coordinate.
thumbnail: tilequeryElevationMarker
topics:
- data
- web apps
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

在本教程中，您将使用[Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery)和 [Mapbox Terrain vector tileset](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/)来创建应用，当用户单击地图上的某个点时，可以返回该点的高程。

{{
  <DemoIframe src="/help/demos/find-elevations-with-tilequery-api/index.html" />
}}

## 开始
要完成本教程，您需要：
- **一个Mapbox访问令牌。**您的访问令牌位于您的账号页面。
- **Mapbox GL JS。**Mapbox GL JS 是用于构建 Web 地图的 JavaScript API。
- **Mapbox Tilequery API。**该 Tilequery API 允许您基于给定的经纬度，从一个矢量瓦片数据集中检索特定要素的相关数据。
- **Mapbox地形矢量瓦片数据。** Mapbox 地形矢量瓦片数据集提供地形数据，包括等高线。
- **jQuery。**jQuery 是一个 JavaScript 库，可以将您的API请求添加到应用程序中。
- **文本编辑器。**使用您选择的文本编辑器编写 HTML，CSS 和 JavaScript。
## 创建地图
首先，您将使用 Mapbox GL JS(https://docs.mapbox.com/mapbox-gl-js/api/) 创建地图。
打开文本编辑器并创建一个名为 `index.html` 的新文件。将下面的代码粘贴到刚创建的 `index.html` 文件中。这些代码创建了页面的结构。还在页面的 `<head>` 中引入了Mapbox GL JS和jQuery。Mapbox GL JS 的 JS 和 CSS 文件允许您使用 Mapbox GL JS 中的方法和样式，而 jQuery将允许您使用[Ajax](https://api.jquery.com/jquery.ajax/)来解析您对 Tilequery API 调用。

同时，在页面的 `<body>` 中还有一个 ID 值为 `map` 的 `<div>` 元素。 此 `<div>` 是地图显示在页面上的容器。
```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Find elevations with the Tilequery API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <script
  src='https://code.jquery.com/jquery-3.4.1.min.js'></script>
  <style>
    body {
      margin: 0;
      padding: 0;
    }

    #map {
      position: absolute;
      top: 0;
      bottom: 0;
      width: 100%;
    }
  </style>
</head>

<body>

  <div id='map'></div>
  
  <script>
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.43877, 37.75152], // Specify the starting position [lng, lat]
      zoom: 11.5 // Specify the starting zoom
    });
  </script>
  
</body>

</html>    
```

此 Mapbox GL JS 代码将地图的样式设置为[Mapbox Outdoors](https://docs.mapbox.com/api/maps/#mapbox-styles)，为其提供居中的坐标，并设置缩放级别。

保存。 在浏览器中打开 HTML 文件，查看以旧金山为中心的地图。

## 用户点击获取坐标
在此应用程序中，当用户单击地图时，将生成 Tilequery API 请求中使用的坐标。想要获得这些坐标，您需要创建一个 `map.on（'click'）` 函数，该函数将获取点击位置的经、纬度。在您的HTML文件中的结束 `</script>` 标记上方添加以下 JavaScript 代码：
```js
// Create variables for the latitude and longitude
var lng;
var lat;

map.on('click', function(e) {
  // When the map is clicked, set the lng and lat variables equal to the lng and lat properties in the returned lngLat object
  lng = e.lngLat.lng;
  lat = e.lngLat.lat;
  console.log(lng + ', ' + lat);
});
```

当点击地图时，返回的事件包括 Mapbox GL JS 的一个[`lngLat`对象](https://docs.mapbox.com/mapbox-gl-js/api/#lnglat)，它包含点击点的经、纬度。`map.on（'click'）` 函数将这些属性赋值给 `lng`、`lat` 变量。

保存，然后刷新您的浏览器页面并打开开发者工具。当您单击地图时，您的应用程序会将点击点的经、纬度打印到 JavaScript 控制台。

{{
<AppropriateImage imageId="tilequeryElevationLngLatOnClick" alt="Screenshot showing two coordinate pairs printed to the developer console" />
}}

## 添加侧边栏

在您的 HTML 文件的 `<body>` 中，添加一个新的 `<div>` 标签。这个 `<div>` 标签将用于显示点击的点的经度，纬度和高程：

```html
<div class="eleInfo">
  <div>Longitude:&nbsp;<span id='lng'></span></div>
  <div>Latitude:&nbsp;<span id='lat'></span></div>
  <div>Elevation:&nbsp;<span id='ele'></span></div>
</div>
```

对新的 `<div>` 设置样式，请将以下的 CSS 代码添加到您的 HTML 文件的 `<style>` 中：
```css
.eleInfo {
  position: absolute;
  font-family: sans-serif;
  margin-top: 5px;
  margin-left: 5px;
  padding: 5px;
  width: 200px;
  border: 2px solid black;
  font-size: 20px;
  color: #222;
  background-color: #fff;
}
```

最后，创建三个新变量，用于接收新的 `<span>` 标签的 ID 值。在您的 JavaScript 中，在 `lng` 和 `lat` 变量下面添加以下代码：

```js
var lngDisplay = document.getElementById('lng');
var latDisplay = document.getElementById('lat');
var eleDisplay = document.getElementById('ele');
```

保存并刷新页面。添加的侧边栏将位于页面的左侧。接下来，您可以通过创建的 `<span>` 标签的 ID 值在侧栏中显示经度、纬度和高程。

{{
<AppropriateImage imageId="tilequeryElevationSidebar" alt="Screenshot showing a sidebar on the map that contains the words Longitude, Latitude, and Elevation" />
}}

## Tilequery API请求格式
[Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery)允许您基于给定的经纬度，从一个矢量瓦片数据集中检索特定要素的相关数据。

一个Tilequery请求有两个**必需**的参数：
- **`tileset_id`:** 要查询的瓦片数据的标识符。
- **`{lon, lat}`:** 查询点的坐标。

在本教程中，您将可以使用到两个**可选**参数：
- **`limit`:** 此参数允许您指定查询可以返回的最大结果数。默认结果数为5，最大为50。
- **`layers`:** 此参数允许您仅返回查询瓦片数据中的特定图层的结果。
一个对 Tilequery API 的调用示例，`limit` 值设置为50，并且只返回来自 `contour` 层的结果如下所示：

```
https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/-105.01109,39.75953.json?layers=contour&limit=50&access_token={{ <UserAccessToken /> }}
```

一个 Tilequery API 请求返回的是以 `{lon}，{lat}` 描述的地理点或其附近要素的[GeoJSON `FeatureCollection`](https://tools.ietf.org/html/rfc7946#section-3.3)。想要了解更多有关Tilequery API的信息，比如其他可选参数及其响应对象，请浏览[Tilequery API documentation](https://docs.mapbox.com/api/maps/#tilequery)。

## Mapbox地形瓦片数据
在本教程中，您将使用 Tilequery API 来查询[Mapbox Terrain](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/)矢量瓦片数据，其中包括地形，山体阴影和土地覆盖等要素。具体来说，您将使用 `layers` 参数返回 `contour` [source layer](https://docs.mapbox.com/help/glossary/source-layer/)中的要素，其中包含名为 [`ele`](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/#elevation)的属性。此属性是以米为单位的高程值，对应10米的高度增量。

在 Mapbo x地形矢量瓦片数据中， `contour` 由堆叠的多边形组成。这意味着查询 Mapbox 地形矢量瓦片数据的大多数 Tilequery API 请求，将会返回 `contour`图层中的多个要素。由于所需的高程数据包含在 `contour` 图层中，因此需要解析返回的 GeoJSON，以将要素与 `contour` 图层分离，并找到最大高程值。

{{<Note title="Mapbox地形矢量瓦片数据中的高程值限制" imageComponent={<BookImage />}>}}
Tilequery API的 `limit` 参数允许在一个响应中使用50个或更少的要素。由于本教程使用 Mapbox 地形矢量瓦片数据，其中包括10米增量的高程数据，因此返回的50个要素可能不足以返回某些高海拔位置的最大值。

此外，由于高程以10米为增量返回，因此结果可能会存在一些误差。比如，一座高264米的山返回的最大海拔可能是260米。Mapbox 没有任何其他矢量数据源具有比地形瓦片数据中可用的高程数据精度更高。

如果您对高程变化较大的区域使用 Tilequery API，或者需要获取精确高程，我们建议您使用 Tilequery API 查询包含此信息的自定义瓦片数据。
{{</Note>}}


## 添加Tilequery API调用
您已经创建了用户单击地图时捕获经、纬度的变量。在此步骤中，您将在调用[Tilequery API](https://docs.mapbox.com/api/maps/#tilequery)时使用这些 `lng` 和 `lat` 变量。

定义一个方法 `getElevation（）`，并使用 `lng` 和 `lat` 值构造 Tilequery API 请求，然后使用 Ajax 发送请求并检索结果。将以下代码添加到您的 JS 代码的结束 `</ script>` 标签标记之前：

```js
function getElevation() {
  // Construct the API request
  var query = 'https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/' + lng + ',' + lat + '.json?layers=contour&limit=50&access_token=' + mapboxgl.accessToken;
  $.ajax({
    method: 'GET',
    url: query,
  }).done(function(data) {
    // Get all the returned features
    var allFeatures = data.features;
    console.log(allFeatures);
    // Create an empty array to add elevation data to
    var elevations = [];
    // For each returned feature, add elevation data to the elevations array
    for (i = 0; i < allFeatures.length; i++) {
      elevations.push(allFeatures[i].properties.ele);
    }
    console.log(elevations);
    // In the elevations array, find the largest value
    var highestElevation = Math.max(...elevations);
    console.log(highestElevation);
  });
}
```

Tilequery API 返回要素对象。由于此查询中的要素对象来自 `contour` 图层，因此每个要素对象都包含一个 `properties.ele` 值。

对于 `allFeatures` 中的每一项，此代码段采用 `properties.el` 值并将其添加到 `elevations `数组。然后，使用[`Math.max`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max)和[spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) `(...elevations)`，将 `highestElevation` 变量设置为 `elevations` 数组中的最大值。

现在，您需要在用户单击地图时调用 `getElevation()` 方法。更新 `map.on（'click'）` 函数：

```js
map.on('click', function(e) {
  lng = e.lngLat.lng;
  lat = e.lngLat.lat;
  
  getElevation();
});
```

保存并打开开发者工具。在浏览器中刷新页面，然后单击地图。点击后，三个变量将打印到控制台：
- `allFeatures`: 包含调用 Tilequery API 返回的所有要素对象。您可以浏览每个要素对象以查看该要素的 `properties.ele` 值。
- `elevations`: 包含每个 `properties.ele` 值。
- `highestElevation`: 高程中的最大值，因此也是 Tilequery API 为请求坐标返回的最高点。

{{
<AppropriateImage imageId="tilequeryElevationElevationOnClick" alt="Screenshot showing the browser's develper tools, to which all the feature objects, their elevations, and the highest returned elevation have been printed" />
}}

## 显示返回值
您已经看到打印在控制台的 Tilequery API 请求结果，接下来是将它们显示在之前创建的侧栏中。更新 `getElevation（）` 方法：

```js
function getElevation() {
  // make API request
  var query = 'https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/' + lng + ',' + lat + '.json?layers=contour&limit=50&access_token=' + mapboxgl.accessToken;
  $.ajax({
    method: 'GET',
    url: query,
  }).done(function(data) {
    // Display the longitude and latitude values
    lngDisplay.textContent = lng.toFixed(2);
    latDisplay.textContent = lat.toFixed(2);
    // Get all the returned features
    var allFeatures = data.features;
    // Create an empty array to add elevation data to
    var elevations = [];
    // For each returned feature, add elevation data to the elevations array
    for (i = 0; i < allFeatures.length; i++) {
      elevations.push(allFeatures[i].properties.ele);
    }
    // In the elevations array, find the largest value
    var highestElevation = Math.max(...elevations);
    // Display the largest elevation value
    eleDisplay.textContent = highestElevation + ' meters';
  });
}
```

此更新函数分别将 `lngDisplay` 和 `latDisplay的 `值设置为单击时的经度和纬度，并使用[`toFixed(2)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) 将显示的值限制为两个小数点。它还将 `eleDisplay` 的值设置为`highestElevation`。

保存更改并在浏览器中刷新页面。现在，当您单击地图上的某个位置时，其经度，纬度和高程将显示在侧边栏中。

{{
<AppropriateImage imageId="tilequeryElevationSidebarDisplay" alt="Screenshot showing the sidebar, with a clicked point's longitude, latitude, and elevation displayed" />
}}

## 在点击的位置添加标记

最后一步是在用户点击的坐标处向地图添加标记。这将有助于用户更好地识别他们获取坐标和高程数据的位置。

在 `map.on（'click'）` 函数之前，将以下代码添加到 javascript 中：

```js
var marker = new mapboxgl.Marker({
  'color': '#314ccd'
});
```

您可以使用单击地图时返回的Mapbox GL JS [`lngLat` object](https://docs.mapbox.com/mapbox-gl-js/api/#lnglat)来设置标记的位置。要在点击的坐标地图上绘制标记，请在 `map.on（'click'）` 方法中添加以下代码：

```js
marker.setLngLat(e.lngLat).addTo(map);
```

保存并刷新页面。现在，当您单击地图时，您将在单击的坐标处看到一个蓝色标记。
{{
<AppropriateImage imageId="tilequeryElevationMarker" alt="Screenshot showing the map with a marker at the clicked location" />
}}

## 最终结果
您已创建一个应用程序，该应用程序返回单击点的高程并将其显示在地图上。
{{
  <DemoIframe src="/help/demos/find-elevations-with-tilequery-api/index.html" />
}}

最终的 HTML 文件如下所示：

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Find elevations with the Tilequery API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <script
  src='https://code.jquery.com/jquery-3.4.1.min.js'></script>
  <style>
    body {
      margin: 0;
      padding: 0;
    }

    #map {
      position: absolute;
      top: 0;
      bottom: 0;
      width: 100%;
    }
    
    .eleInfo {
      position: absolute;
      font-family: sans-serif;
      margin-top: 5px;
      margin-left: 5px;
      padding: 5px;
      width: 200px;
      border: 2px solid black;
      font-size: 20px;
      color: #222;
      background-color: #fff;
    }
  </style>
</head>

<body>

  <div id='map'></div>
  <div class="eleInfo">
    <div>Longitude:&nbsp;<span id='lng'></span></div>
    <div>Latitude:&nbsp;<span id='lat'></span></div>
    <div>Elevation:&nbsp;<span id='ele'></span></div>
  </div>
  <script>
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.43877, 37.75152], // Specify the starting position [lng, lat]
      zoom: 11.5 // Specify the starting zoom
    });
    
    var lng;
    var lat;
    var lngDisplay = document.getElementById('lng');
    var latDisplay = document.getElementById('lat');
    var eleDisplay = document.getElementById('ele');
    
    var marker = new mapboxgl.Marker({
      'color': '#314ccd'
    });

    map.on('click', function(e) {
      // Use the returned LngLat object to set the marker location
      // https://docs.mapbox.com/mapbox-gl-js/api/#lnglat
      marker.setLngLat(e.lngLat).addTo(map);
      
      // Create variables set to the LngLat object's lng and lat properties
      lng = e.lngLat.lng;
      lat = e.lngLat.lat;
      
      getElevation();
    });

    function getElevation() {
      // Make the API request
      var query = 'https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/' + lng + ',' + lat + '.json?layers=contour&limit=50&access_token=' + mapboxgl.accessToken;
      $.ajax({
        method: 'GET',
        url: query,
      }).done(function(data) {
        // Display the longitude and latitude values
        lngDisplay.textContent = lng.toFixed(2);
        latDisplay.textContent = lat.toFixed(2);
        // Get all the returned features
        var allFeatures = data.features;
        // Create an empty array to add elevation data to
        var elevations = [];
        // For each returned feature, add elevation data to the elevations array
        for (i = 0; i < allFeatures.length; i++) {
          elevations.push(allFeatures[i].properties.ele);
        }
        // In the elevations array, find the largest value
        var highestElevation = Math.max(...elevations);
        // Display the largest elevation value
        eleDisplay.textContent = highestElevation + ' meters';
      });
    }
  </script>

</body>

</html>
```

## 下一步
要构建本教程中使用的工具和技术，请浏览以下资源：
- 有关如何使用可选参数的更多信息，请浏览[Tilequery API documentation](https://docs.mapbox.com/api/maps/#tilequery)。
- 通过[Create a timezone finder with the Tilequery API](https://docs.mapbox.com/help/tutorials/create-a-timezone-finder-with-mapbox-tilequery-api/)教程，了解如何在地图外部使用Tilequery API。
- 通过[Make a healthy food finder with the Tilequery API](https://docs.mapbox.com/help/tutorials/tilequery-healthy-food-finder/)  教程，了解如何结合使用Tilequery API和Mapbox Geocoding API来查询自定义瓦片数据的结果。
- 如果使用Tilequery API查询的Mapbox地形矢量瓦片数据的高程等级不能满足您的需求，您可以查阅[alternative method of retrieving elevation data](https://docs.mapbox.com/help/troubleshooting/access-elevation-data/#mapbox-terrain-rgb) ，使用Mapbox Terrain-RGB（一种栅格切片集）来代替。
