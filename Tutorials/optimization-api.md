---
title: 生成优化路线
description: 使用 Mapbox Optimization API 在几个点之间生成持续时间优化的路线。
thumbnail: optimizationApi
level: 3
platform: web
topics:
- web apps
- directions
language:
- JavaScript
prereq: 需要较高 JavaScript 技能.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

Mapbox Optimization API 返回最多12个坐标之间的持续时间优化路线。在本指南中，您将构建一个应用程序，允许您单击地图上的多个点并使用Optimization API创建优化的交付路径。

{{
  <DemoIframe src="/help/demos/optimization-api/step-five.html" />
}}

在整个指南中，您将创建一个自定义标记来表示送货车辆，向地图添加仓库位置，在用户点击地图时添加标记图标，并在这些点之间实时构建优化路线。

## 开始着手

以下是您将在本指南中使用的资源：

- **Mapbox 账号及 access token** 在 [mapbox.com/signup](https://www.mapbox.com/signup/) 注册一个账户. 你可以在[Account page](https://account.mapbox.com/) 中找到你的 [access tokens](/help/how-mapbox-works/access-tokens/) 。
- **Mapbox GL JS** [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/) 是我们的 JavaScript 库，它使用WebGL基于Mapbox GL样式呈现交互式Web地图。
- **Turf.js** [Turf](http://turfjs.org/) 是一个 JavaScript 库，这允许你向地图添加地理空间分析的功能。
- **Mapbox Optimization API** 我们的 [Optimization API](https://docs.mapbox.com/api/navigation/#optimization) 将帮助您为整个车队的多个站点生成最佳的交付路线。
- **jQuery** [jQuery](https://jquery.com/) 是一个 JavaScript 库，这允许你将您的API请求添加到您的应用程序。

## 初始化地图

首先使用Mapbox GL JS初始化地图。创建一个新的HTML文件，并使用下面的代码初始化以密歇根州底特律市为中心的地图。此代码还引用了`head`中的几个脚本，并声明了稍后步骤中需要的一些JavaScript变量。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Delivery App</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
    <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js'></script>
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <style>

      body {
        margin: 0;
        padding: 0;
      }

      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
      }
    </style>
  </head>
  <body>
    <div id='map' class='contain'></div>
    <script>
      var truckLocation = [-83.093, 42.376];
      var warehouseLocation = [-83.083, 42.363];
      var lastQueryTime = 0;
      var lastAtRestaurant = 0;
      var keepTrack = [];
      var currentSchedule = [];
      var currentRoute = null;
      var pointHopper = {};
      var pause = true;
      var speedFactor = 50;

      // Add your access token
      mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

      // Initialize a map
      var map = new mapboxgl.Map({
        container: 'map', // container id
        style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}', // stylesheet location
        center: truckLocation, // starting position
        zoom: 12 // starting zoom
      });
    </script>
  </body>
</html>
```

在浏览器中打开文件，您将看到以底特律为中心的地图。

{{
  <DemoIframe src="/help/demos/optimization-api/step-one.html" />
}}

## 设定地图

接下来，添加送货卡车的位置和取货地点。

### 添加卡车位置


有很多方法可以使用 Mapbox GL JS 添加点数据。在本指南中，您将为每个标记创建一个 HTML DOM 元素，并使用 Mapbox GL JS 的 [`Marker`](https://www.mapbox.com/mapbox-gl-js/api/#marker)方法将其绑定到一个坐标上。当使用 Marker 方法添加标记时，将附加一个空的`div`到该点。在将标记添加到地图之前，您需要指定标记的样式。

首先在`style`标签之间添加`truck`类。

```css
.truck {
  margin: -10px -10px;
  width: 20px;
  height: 20px;
  border: 2px solid #fff;
  border-radius: 50%;
  background: #3887be;
  pointer-events: none;
}
```


接下来，使用`mapboxgl.Marker`将标记添加到地图中。为了确保代码的其余部分可以执行，它需要存在于地图加载完成时执行的 *回调函数（callback function）* 。

{{
  <Note
    imageComponent={<BookImage />}
    title='什么是回调？'
  >
    <p>在页面上初始化地图不仅仅是在<code>map</code>div中创建容器，它还告诉浏览器请求您在第1部分中创建的 Mapbox Studio 样式。这可能需要不同的时间，具体取决于Mapbox服务器响应该请求的速度，以及代码中您要添加的其他所有内容都取决于上述样式是否已加载到地图上。因此，在执行更多代码之前确保加载样式非常重要。</p><p>幸运的是，地图对象可以告诉您的浏览器有关地图状态发生变化时发生的某些事件。其中一个事件是<code>load</code>，它在样式加载到地图时发出。当您使用<code>map.on</code>方法时，您可以确保*仅*在地图完成加载后执行其余代码，方法是将其置于<a href='https://github.com/maxogden/art-of-node#callbacks'>回调函数</a>中，该函数在<code>load</code>事件发生时被调用。</p>
  </Note>
}}

在上一步中，您声明了一个名为`truckLocation`的变量，该变量是一组包含两个数字（经度和纬度）的数组。 通过`setLngLat`，使用`truckLocation`作为卡车标记的坐标。

{{
  <Note
    imageComponent={<BookImage />}
  >
    <p>在本指南中，您使用静态点作为送货卡车的位置。在您自己的应用程序中，您可以使用物理设备的位置设置经度和纬度，例如手机或平板电脑的位置，从物联网设备收集上报数据，或从车辆收集GPS信号。</p> 
  </Note>
}}

加载地图后，使用以下代码添加标记。

```js
map.on('load', function() {
  var marker = document.createElement('div');
  marker.classList = 'truck';

  // Create a new marker
  truckMarker = new mapboxgl.Marker(marker)
    .setLngLat(truckLocation)
    .addTo(map);
});
```


### 添加仓库位置

现在将仓库位置添加到地图中。这将是送货卡车必须去装货的地方。首先创建一个GeoJSON 要素集，其中包含描述仓库所在位置的单个点要素。[Turf.js](http://turfjs.org) 的 `featureCollection`方法是将坐标或一系列坐标转换为GeoJSON要素集的便捷方法。在你的`map.on('load', function(){});`回调之前添加下面的代码。请注意，`warehouseLocation`变量是你复制的第一个代码块中在初始化地图时声明的纬度，经度对。

```js
// Create a GeoJSON feature collection for the warehouse
var warehouse = turf.featureCollection([turf.point(warehouseLocation)]);
```

然后，在 `map.on('load', function())` 回调中，创建两个新图层 &mdash; 圆形图层和符号图层。两个层都将使用`warehouse` GeoJSON要素集作为数据源。

```js
// Create a circle layer
map.addLayer({
  id: 'warehouse',
  type: 'circle',
  source: {
    data: warehouse,
    type: 'geojson'
  },
  paint: {
    'circle-radius': 20,
    'circle-color': 'white',
    'circle-stroke-color': '#3887be',
    'circle-stroke-width': 3
  }
});

// Create a symbol layer on top of circle layer
map.addLayer({
  id: 'warehouse-symbol',
  type: 'symbol',
  source: {
    data: warehouse,
    type: 'geojson'
  },
  layout: {
    'icon-image': 'grocery-15',
    'icon-size': 1
  },
  paint: {
    'text-color': '#3887be'
  }
});
```

刷新您的应用程序，您将看到一张显示送货卡车和仓库位置的地图。

{{
  <DemoIframe src="/help/demos/optimization-api/step-two.html" />
}}

## 添加送货位置（单击时）

在一个在多个点之间生成优化路径的应用程序中，有许多不同的方法可以生成点：用户可以输入地址，用户可以选择地图上的坐标，或者可以从外部源提取数据。在本指南中，您将允许用户通过单击地图来选择点。

对 Optimization API 的请求必须包含2-12个坐标。在本指南中：

- 你将使用默认的`roundtrip=true`。这意味着第一个坐标是行程的起点和终点。（如果送货卡车需要返回车库，这将非常有用。）起点和终点都将计入12个坐标的总限制。
- 取货位置也将计入12个坐标的总限制。
- 因此，用户可以选择最多9个点 &mdash; 12个坐标限制减去卡车位置作为开始和结束（2个坐标）和取货位置（1个坐标）。


### 建立新图层

首先创建一个包含所有送货位置的新图层。

创建一个空的 GeoJSON 要素集。稍后，当您单击地图时，您将在此要素集中存储送货位置。可以直接在上面添加的`warehouse`变量之后添加它。

```js
// Create an empty GeoJSON feature collection for drop-off locations
var dropoffs = turf.featureCollection([]);
```

然后，在 `map.on('load', function())` 中添加一个名为 `dropoffs-symbol` 的新图层，它将显示所有的送货位置。Mapbox GL JS中的图层需要`source`，但用户尚未选择任何送货位置，因此您需要提供一个空的 GeoJSON 要素集作为起始数据。首次初始化地图时，数据源将是您在上面定义的空 `dropoffs` 要素集。随后，在用户单击地图后，单击的点将添加到 `dropoffs` 要素集中，并且图层的数据源将更新。

```js
map.addLayer({
  id: 'dropoffs-symbol',
  type: 'symbol',
  source: {
    data: dropoffs,
    type: 'geojson'
  },
  layout: {
    'icon-allow-overlap': true,
    'icon-ignore-placement': true,
    'icon-image': 'marker-15',
  }
});
```

### 添加单击事件监听

您需要在监听用户对地图的单击操作。在 `map.on('load', function())` 回调中添加一个单击监听器。在单击监听器中，添加两个新函数`newDropoff`和`updateDropoffs`，每次单击地图时都会调用它们。

```js
// Listen for a click on the map
map.on('click', function(e) {
  // When the map is clicked, add a new drop-off point
  // and update the `dropoffs-symbol` layer
  newDropoff(map.unproject(e.point));
  updateDropoffs(dropoffs);
});
```

构建 `newDropoff` 和 `updateDropoffs` 函数。当用户点击地图时，您将产生新的送货请求。当用户发出新请求时，会发生两件事：您将创建一个新的送货位置，并且您将更新`dropoffs-symbol`图层的数据源。

在 `map.on('load', function())` 回调之外添加以下代码。

```js
function newDropoff(coords) {
  // Store the clicked point as a new GeoJSON feature with
  // two properties: `orderTime` and `key`
  var pt = turf.point(
    [coords.lng, coords.lat],
    {
      orderTime: Date.now(),
      key: Math.random()
    }
  );
  dropoffs.features.push(pt);
}

function updateDropoffs(geojson) {
  map.getSource('dropoffs-symbol')
    .setData(geojson);
}
```

刷新您的应用程序。单击地图时，作为送货位置的新标记符号将添加到地图中。

{{
  <DemoIframe src="/help/demos/optimization-api/step-three.html" />
}}

## 生成并添加路线

接下来，您将构建对 Optimization API 的请求，将响应中的路线添加到地图中，并为路线设置样式。

### 创建一个仅有空源的图层

与上一步中一样，创建一个空的GeoJSON要素集，稍后将包含单击地图后生成的路线。在声明`dropoffs`变量后立即添加此行代码。

```js
// Create an empty GeoJSON feature collection, which will be used as the data source for the route before users add any new data
var nothing = turf.featureCollection([]);
```

在 `map.on('load', function())` 中，直接在您编写的仓库图层代码之后，添加一个有着空源的图层。在发出API请求后，您将使用它来显示路线。

```js
map.addSource('route', {
  type: 'geojson',
  data: nothing
});

map.addLayer({
  id: 'routeline-active',
  type: 'line',
  source: 'route',
  layout: {
    'line-join': 'round',
    'line-cap': 'round'
  },
  paint: {
    'line-color': '#3887be',
    'line-width': [
      "interpolate",
      ["linear"],
      ["zoom"],
      12, 3,
      22, 12
    ]
  }
}, 'waterway-label');
```

### 构建请求

接下来，构建对 Optimization API 的请求以生成路线。您的请求将包含以下几个参数：

- `profile`: 这是交通方式。你将使用`driving`。
- `coordinates`: 这是一个以分号分隔的 `{longitude},{latitude}` 坐标列表。必须有2到12个坐标。在本指南中，坐标列表包括卡车的起始位置，仓库，最多九个送货位置以及卡车起动的位置。
- `distributions`: 这是一个以分号分隔的数字对列表，与坐标列表对应。第一个数字表示坐标列表中取货位置坐标的索引，第二个数字表示坐标列表中送货位置坐标的索引。每对必须包含两个数字。一对中的取送位置不能相同。返回的解决方案将在访问送货地点之前访问取货地点。

在上一节中添加的`updateDropoffs`函数后添加以下内容。

```js
// Here you'll specify all the parameters necessary for requesting a response from the Optimization API
function assembleQueryURL() {

  // Store the location of the truck in a variable called coordinates
  var coordinates = [truckLocation];
  var distributions = [];
  keepTrack = [truckLocation];

  // Create an array of GeoJSON feature collections for each point
  var restJobs = objectToArray(pointHopper);

  // If there are any orders from this restaurant
  if (restJobs.length > 0) {

    // Check to see if the request was made after visiting the restaurant
    var needToPickUp = restJobs.filter(function(d, i) {
      return d.properties.orderTime > lastAtRestaurant;
    }).length > 0;

    // If the request was made after picking up from the restaurant,
    // Add the restaurant as an additional stop
    if (needToPickUp) {
      var restaurantIndex = coordinates.length;
      // Add the restaurant as a coordinate
      coordinates.push(warehouseLocation);
      // push the restaurant itself into the array
      keepTrack.push(pointHopper.warehouse);
    }

    restJobs.forEach(function(d, i) {
      // Add dropoff to list
      keepTrack.push(d);
      coordinates.push(d.geometry.coordinates);
      // if order not yet picked up, add a reroute
      if (needToPickUp && d.properties.orderTime > lastAtRestaurant) {
        distributions.push(restaurantIndex + ',' + (coordinates.length - 1));
      }
    });
  }

  // Set the profile to `driving`
  // Coordinates will include the current location of the truck,
  return 'https://api.mapbox.com/optimized-trips/v1/mapbox/driving/' + coordinates.join(';') + '?distributions=' + distributions.join(';') + '&overview=full&steps=true&geometries=geojson&source=first&access_token=' + mapboxgl.accessToken;
}

function objectToArray(obj) {
  var keys = Object.keys(obj);
  var routeGeoJSON = keys.map(function(key) {
    return obj[key];
  });
  return routeGeoJSON;
}
```

### 发送请求

通过 [jQuery](https://api.jquery.com/jquery.ajax/) 发送请求。以下代码中完成了几件事情：

- **生成请求**。 使用您在上一步中 `assembleQueryURL()` 函数生成的 URL 向 Optimization API 发出请求。
- **生成 GeoJSON 要素集**。 API响应将包含一个`trips`数组。使用此数组中的第一个行程（`trips[0]`）创建包含路径的GeoJSON要素集。
- **更新路线数据**。在用户与地图交互之前，`route` 源是一个空的GeoJSON要素集。将`route`源从空要素集更新为API响应中返回的`trip`。然后检查是否存在行程：
  - 如果没有可用的行程，请使用空的 `nothing` 源。
  - 如果有行程，请获取`route`源并将数据设置为`routeGeoJSON`。
- **达到坐标限制时显示警告消息**。用户可以在地图上选择最多九个点。当用户达到该限制时，显示一条警告消息，表明他们无法再向路线添加任何点。


所有这些都将在现有的`newDropoff`函数中发生，这意味着每次指定新的送货位置时都会向Optimization API发出请求 &mdash; 即用户每次点击地图时。

更新现有的`newDropoff`函数，使用下面的代码添加API请求。

```js
function newDropoff(coords) {
  // Store the clicked point as a new GeoJSON feature with
  // two properties: `orderTime` and `key`
  var pt = turf.point(
    [coords.lng, coords.lat],
    {
      orderTime: Date.now(),
      key: Math.random()
    }
  );
  dropoffs.features.push(pt);
  pointHopper[pt.properties.key] = pt;

  // Make a request to the Optimization API
  $.ajax({
    method: 'GET',
    url: assembleQueryURL(),
  }).done(function(data) {
    // Create a GeoJSON feature collection
    var routeGeoJSON = turf.featureCollection([turf.feature(data.trips[0].geometry)]);

    // If there is no route provided, reset
    if (!data.trips[0]) {
      routeGeoJSON = nothing;
    } else {
      // Update the `route` source by getting the route source
      // and setting the data equal to routeGeoJSON
      map.getSource('route')
        .setData(routeGeoJSON);
    }

    if (data.waypoints.length === 12) {
      window.alert('Maximum number of points reached. Read more at docs.mapbox.com/api/navigation/#optimization.');
    }
  });
}
```

刷新您的应用程序，在地图上选择点，您将看到在所有点之间绘制的路线。

{{
  <DemoIframe src="/help/demos/optimization-api/step-four.html" />
}}

### 为路线添加方向性

对于当前的风格，理解路线的方向时会有点困难。添加另一个名为`routearrows`的图层，以帮助地图用户了解卡车是如何在路线上行驶的。`routearrows`层将使用与`routeline-active`层相同的数据源。使用带箭头的符号图层代替线图层，箭头指示沿线的路线的方向性。

在 `map.on('load', function())` 回调函数中添加以下代码。

```js
map.addLayer({
  id: 'routearrows',
  type: 'symbol',
  source: 'route',
  layout: {
    'symbol-placement': 'line',
    'text-field': '▶',
    'text-size': [
      "interpolate",
      ["linear"],
      ["zoom"],
      12, 24,
      22, 60
    ],
    'symbol-spacing': [
      "interpolate",
      ["linear"],
      ["zoom"],
      12, 30,
      22, 160
    ],
    'text-keep-upright': false
  },
  paint: {
    'text-color': '#3887be',
    'text-halo-color': 'hsl(55, 11%, 96%)',
    'text-halo-width': 3
  }
}, 'waterway-label');
```

刷新您的应用程序，在地图上选择点，您将看到在所有点之间绘制箭头的路线。

## 最终成果

您使用 Optimization API 构建了一个Web应用程序，允许用户在地图上选择多个点，发出API请求，并实时显示经过优化的路径。

{{
  <DemoIframe src="/help/demos/optimization-api/step-five.html" />
}}

## 了解更多

阅读 [Mapbox Optimization API documentation](https://docs.mapbox.com/api/navigation/#optimization) 来获取更多资讯，或通过我们的分步教程，学习如何为 iOS 和 Android 构建行车用的应用程序：

- [Build a navigation app for iOS](/help/tutorials/ios-navigation-sdk)
- [Build a navigation app for Android](/help/tutorials/android-navigation-sdk)
