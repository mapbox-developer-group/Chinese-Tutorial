---
title: Getting started with the Mapbox Directions API
description: Add routing capabilities to your application with the Mapbox Directions API.
thumbnail: directionsApi
level: 1
language:
- JavaScript
topics:
- directions
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

[Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) 能为用户提供路线、拐弯指引和行程持续时间。本教程将引导你完成请求路线的过程、在固定位置和点击位置间添加单条自行车路线的过程，以及显示路线逐向指引的过程。

{{
  <DemoIframe src="/help/demos/directions-api/index.html" />
}}

## 入门

以下是入门前需要的一些资源：

- [**一个 access token**](/help/glossary/access-token/) 由你个人账号提供。你将使用 access token 将地图与个人账号关联，你可以在 [Account page](https://www.mapbox.com/account/) 找到它。
- [**Mapbox Directions API 文档**](https://docs.mapbox.com/api/navigation/#directions) 一份参考，提供发送请求时的所有可用选项以及应答的解析。
- [__Mapbox GL JS__](https://docs.mapbox.com/mapbox-gl-js/overview/) 使用 WebGL 从 Mapbox GL 样式来渲染交互式地图的 Mapbox JavaScript 库。
- __一个文本编辑器__ 你将编写 HTML、 CSS 和 JavaScript。

## 建立一个 Directions API 请求

向任何 Mapbox web 服务发出请求时，请求 URL 的一般结构会这样开始：

```
https://api.mapbox.com/{service}/
```

在这种情况下，`{service}` 将是 `directions`，但你也可以请求 `styles`、 `geocoding` 和其他 Mapbox API。

下一部分将是版本号，它有助于了解一些信息。因为 API 可能会随着时间的推移而更改，为你提供更强大的功能或更改请求的工作方式。Directions API 当前版本是 `v5`：

```
https://api.mapbox.com/directions/v5/
```

### 参数

如果你尝试将上述 URL 粘贴到浏览器的地址栏中，请求将不会返回任何内容。你仍然需要传递一些参数，这些参数将缩小请求的范围。对于 Mapbox Directions API 而言，你需要为请求提供 **profile**（旅行模式）和 **coordinates**（起点和终点）：

- 在这种情况下，使用 `cycling` 为 profile，会生成自行车路线。
- 使用 `-84.518641, 39.134270` 作为起始坐标，`-84.512023, 39.102779` 作为终点坐标。请注意，这些坐标必须用英文分号 `;` 隔开。
- 使用可选参数 `geometries=geojson` 指定它以 GeoJSON 特性返回路线。

```
https://api.mapbox.com/directions/v5/mapbox/cycling/-84.518641,39.134270;-84.512023,39.102779?geometries=geojson
```

### Access token

剩下的唯一必需项目是你的 access token。为了追踪你的账号 _针对此特定服务_ 发出的请求，需要 access token。你可以为请求创建特定 token 或使用默认 token。

添加此 token 时，在 token 之前使用 `&` 符号，将此标记追加到请求中：

```
https://api.mapbox.com/directions/v5/mapbox/cycling/-84.518641,39.134270;-84.512023,39.102779?geometries=geojson&access_token={{ <UserAccessToken /> }}
```

现在你有一个请求，请将完整的 URL 粘贴到浏览器的地址栏中以获取应答。

## 查看应答

发出请求时，将返回 JSON 对象，包含以下信息：

- **waypoints**：这是一个 _Waypoint_ 对象的数组。此时，数组将包含起点和终点。
- **routes**：这是按推荐等级降序排列的 _Route_ 对象的数组。此时，你没有请求其他路线，因此将只返回一条。你将在下一步中使用 `geometry` 属性在，地图上显示此路线。
- **code**：此字符串表示应答的状态。在正常有效应答中，该值将为 `Ok`。

```json
{
  "waypoints": [
    {
      "location": [
        -84.518399,
        39.134126
      ],
      "name": ""
    },
    {
      "location": [
        -84.511987,
        39.102638
      ],
      "name": "East 6th Street"
    }
  ],
  "routes": [
    {
      "legs": [
        {
          "steps": [],
          "weight": 1332.6,
          "distance": 4205,
          "summary": "",
          "duration": 1126
        }
      ],
      "weight_name": "cyclability",
      "geometry": {
        "coordinates": [
          [
            -84.518399,
            39.134126
          ],
          [
            -84.51841,
            39.133781
          ],
          [
            -84.520024,
            39.133456
          ],
          [
            -84.520321,
            39.132597
          ],
          [
            -84.52085,
            39.128019
          ],
          [
            -84.52036,
            39.127901
          ],
          [
            -84.52094,
            39.122783
          ],
          [
            -84.52022,
            39.122713
          ],
          [
            -84.520768,
            39.120841
          ],
          [
            -84.519639,
            39.120268
          ],
          [
            -84.51233,
            39.114141
          ],
          [
            -84.512652,
            39.11311
          ],
          [
            -84.512399,
            39.112216
          ],
          [
            -84.513232,
            39.112084
          ],
          [
            -84.512127,
            39.107599
          ],
          [
            -84.512904,
            39.107489
          ],
          [
            -84.511692,
            39.102682
          ],
          [
            -84.511987,
            39.102638
          ]
        ],
        "type": "LineString"
      },
      "weight": 1332.6,
      "distance": 4205,
      "duration": 1126
    }
  ],
  "code": "Ok"
}
```

## 建立地图

现在，你已经了解了 Mapbox Directions API 请求和应答的工作原理，因此可以使用此 API 请求将路线添加到 web 地图上。

### 设置 HTML 文件

创建一个名为 `index.html` 的新 HTML 文件，并使用以下代码初始化 Mapbox GL JS 地图。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title></title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
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
        width: 100%;
      }
    </style>
  </head>
  <body>
    <div id='map'></div>
    <script>
    // add the JavaScript here
    </script>
  </body>
</html>
```

接下来，将以下脚本添加到 `<script>` 标签中，初始化地图、样式和起始位置：

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/streets-v10',
  center: [-122.662323, 45.523751], // starting position
  zoom: 12
});
// 设置地图界限
var bounds = [[-123.069003, 45.395273], [-122.303707, 45.612333]];
map.setMaxBounds(bounds);

// 初始化地图 canvas，后面会用它
var canvas = map.getCanvasContainer();

// 随意指定的起始位置始终不变
// 只有终点位置会变
var start = [-122.662323, 45.523751];

// 下一步的代码
```


### 添加路线请求功能

接下来，你将构建一个名为 `getRoute` 的函数来发出 API 请求，并将获得的路线添加为新图层。然后，当地图加载时，调用该函数。

在 `getRoute` 函数中，指定 `start` 和 `end` 坐标。start 是在此函数之外定义的，end 将作为参数传入。使用 [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) 对象发出 API 请求。然后，可以使用应答获取所有相关对象，并使用 geometry 将应答作为图层添加到地图上。_地图加载后_ 执行一次这个请求，获取一条起点和终点在一处的路线。

在之前声明的 start 变量之后添加以下代码：

```js
// 创建一个函数来请求 directions
function getRoute(end) {
  // 使用 cycling profile 发起 directions 请求
  // 随意指定的起始位置始终不变
  // 只有终点位置会变
  var start = [-122.662323, 45.523751];
  var url = 'https://api.mapbox.com/directions/v5/mapbox/cycling/' + start[0] + ',' + start[1] + ';' + end[0] + ',' + end[1] + '?steps=true&geometries=geojson&access_token=' + mapboxgl.accessToken;

  // 发起一个 XHR 请求 https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
  var req = new XMLHttpRequest();
  req.responseType = 'json';
  req.open('GET', url, true);
  req.onload = function() {
    var data = req.response.routes[0];
    var route = data.geometry.coordinates;
    var geojson = {
      type: 'Feature',
      properties: {},
      geometry: {
        type: 'LineString',
        coordinates: route
      }
    };
    // 如果地图上已经有此路线，使用 setData 重置
    if (map.getSource('route')) {
      map.getSource('route').setData(geojson);
    } else { // 否则，发起新的请求
      map.addLayer({
        id: 'route',
        type: 'line',
        source: {
          type: 'geojson',
          data: {
            type: 'Feature',
            properties: {},
            geometry: {
              type: 'LineString',
              coordinates: geojson
            }
          }
        },
        layout: {
          'line-join': 'round',
          'line-cap': 'round'
        },
        paint: {
          'line-color': '#3887be',
          'line-width': 5,
          'line-opacity': 0.75
        }
      });
    }
    // 最后这里添加拐弯指引
  };
  req.send();
}

map.on('load', function() {
  // 发起初次 directions 请求
  // start 和 end 在同一处
  getRoute(start);

  // 地图上添加起始点
  map.addLayer({
    id: 'point',
    type: 'circle',
    source: {
      type: 'geojson',
      data: {
        type: 'FeatureCollection',
        features: [{
          type: 'Feature',
          properties: {},
          geometry: {
            type: 'Point',
            coordinates: start
          }
        }
        ]
      }
    },
    paint: {
      'circle-radius': 10,
      'circle-color': '#3887be'
    }
  });
  // 下一步代码
});
```

{{
  <Note title='Mapbox JavaScript SDK' imageComponent={<BookImage />}>
    <p>Mapbox 还提供 JavaScript SDK、一个 node.js 和浏览器 JavaScript 客户端，可直接在 web 应用程序中与我们的 web 服务进行交互。你可以使用 JavaScript SDK 直接发起 Directions API 请求。有关 Mapbox JavaScript SDK 的更多信息，请参考 <a href="https://github.com/mapbox/mapbox-sdk-js/blob/master/docs/services.md">GitHub 文档</a>。</p>
  </Note>
}}

现在，你已经构造了发出请求并绘制路线的函数，你需要从起点加载初始路线。

要查看这是否正常工作，请打开浏览器的控制台（Mac 上 `Command+Alt+J`、Windows 上 `Ctrl+Alt+J`）。到目前为止编写的应用程序，你都可以在其中进行访问交互。控制台中，键入 `getRoute([-122.677738,45.522458])` 执行你的功能，并传递位于波尔兰市中心（OR）的坐标。如果一切正常，你应该看到一条从河的东侧向西侧的线。

{{
  <DemoIframe src="/help/demos/directions-api/demo-one.html" />
}}

## 添加你的起点和终点

现在，你已经创建了起点（`getRoute(start)`），你将提供允许用户选择终点的方法。添加如下代码，允许用户单击地图并更新终点：

```js
map.on('click', function(e) {
  var coordsObj = e.lngLat;
  canvas.style.cursor = '';
  var coords = Object.keys(coordsObj).map(function(key) {
    return coordsObj[key];
  });
  var end = {
    type: 'FeatureCollection',
    features: [{
      type: 'Feature',
      properties: {},
      geometry: {
        type: 'Point',
        coordinates: coords
      }
    }
    ]
  };
  if (map.getLayer('end')) {
    map.getSource('end').setData(end);
  } else {
    map.addLayer({
      id: 'end',
      type: 'circle',
      source: {
        type: 'geojson',
        data: {
          type: 'FeatureCollection',
          features: [{
            type: 'Feature',
            properties: {},
            geometry: {
              type: 'Point',
              coordinates: coords
            }
          }]
        }
      },
      paint: {
        'circle-radius': 10,
        'circle-color': '#f30'
      }
    });
  }
  getRoute(coords);
});
```

{{
  <DemoIframe src="/help/demos/directions-api/demo-two.html" />
}}

## 添加转弯指引

由于将 `steps=true` 参数添加到初始请求中，因此导航路线的所有指引都可以进行解析。现在，将这些步骤添加到侧边栏，它在被称为 `instructions` 的 div 元素中。

```js
// 获取侧边栏，添加指引
var instructions = document.getElementById('instructions');
var steps = data.legs[0].steps;

var tripInstructions = [];
for (var i = 0; i < steps.length; i++) {
  tripInstructions.push('<br><li>' + steps[i].maneuver.instruction) + '</li>';
  instructions.innerHTML = '<br><span class="duration">Trip duration: ' + Math.floor(data.duration / 60) + ' min 🚴 </span>' + tripInstructions;
}
```

在 directions 应答对象中，拐弯指引存储在 `routes` 属性中。你可以在 `routes` > `legs` > `steps` > `maneuver` 内找到 `instructions`。每个 `instructions` 是一个字符串，描述自行车骑手下一步应该沿着路线做什么。

接下来，添加一些 CSS 设置 `div` 样式，使其显示在地图的左侧，并且具有白色背景。

```css
#instructions {
  position: absolute;
  margin: 20px;
  width: 25%;
  top: 0;
  bottom: 20%;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.9);
  overflow-y: scroll;
  font-family: sans-serif;
  font-size: 0.8em;
  line-height: 2em;
}

.duration {
  font-size: 2em;
}
```

## 成品

你已使用 Mapbox Directions API 和 Mapbox GL JS 将自行车路线添加到地图中。

{{
  <DemoIframe src="/help/demos/directions-api/index.html" />
}}

## 后续步骤

现在你已经练习使用 Mapbox Directions API，请阅读 [Directions API documentation](https://docs.mapbox.com/api/navigation/#directions) 中的其他选项。你还可以尝试向应用程序添加更多详细信息：

- 为起点、终点设置唯一样式。
- 使用 [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding)，根据用户输入分配起点和终点。
- 向拐弯指引添加更多详细信息，如距离和持续时间。
- 探索其他集成 directions 服务的方法，包括逐向指引，在应用程序中引入 [Mapbox GL directions plugin](https://github.com/mapbox/mapbox-gl-directions)、[JavaScript SDK](https://github.com/mapbox/mapbox-sdk-js#mapbox-sdk-js) 以及 Mapbox Navigation SDKs for [iOS](https://docs.mapbox.com/ios/navigation/overview/) 和 [Android](https://docs.mapbox.com/android/navigation/overview/)。

不要忘记探索其他与 directions 相关的服务，如 [Mapbox Matrix API](https://docs.mapbox.com/api/navigation/#matrix) 和 [Optimization API](https://docs.mapbox.com/api/navigation/#optimization)。
