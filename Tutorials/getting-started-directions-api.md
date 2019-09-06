---
title: Mapbox Directions API 入门
description: 通过 Mapbox Directions API 为应用程序添加指路功能。
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

[Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) 能为用户提供路线、转弯指引和行程持续时间。本教程将引导你完成请求路线的过程、在固定位置和单击点位间添加单个自行车路线的过程，以及显示路线逐段指引的过程。

{{
  <DemoIframe src="/help/demos/directions-api/index.html" />
}}

## 入门

以下是入门前需要的一些资源：

- [**访问令牌**](/help/glossary/access-token/) 由你的账号提供。你将使用访问令牌将地图与你的账号关联，你可以在 [Account page](https://www.mapbox.com/account/) 找到它。
- [**Mapbox Directions API 文档**](https://docs.mapbox.com/api/navigation/#directions) 发送请求时的所有可用选项以及如何解释回应的参考。
- [__Mapbox GL JS__](https://docs.mapbox.com/mapbox-gl-js/overview/) 使用 WebGL 从 Mapbox GL 样式来渲染交互式地图的 Mapbox JavaScript 库。
- __文本编辑器__ 你将编写 HTML、 CSS 和 JavaScript。

## 生成一个 Directions API 请求

向任何 Mapbox web 服务发出请求时，请求 URL 的一般结构会这样开头：

```
https://api.mapbox.com/{service}/
```

在这种情况下，`{service}` 将是 `directions`，但你也可以请求 `styles`、 `geocoding` 和其他 Mapbox API。

The next part will be the version number. The version number is helpful to know since the API may change over time and provide you with greater capabilities or change how the requests may work. The current version for directions is `v5`:
下一部分将是版本号，它有助于了解，因为 API 可能会随着时间的推移而更改，为你提供更强大的功能或更改请求的工作方式。Directions API 当前版本是"v5"：

```
https://api.mapbox.com/directions/v5/
```

### 参数

如果你尝试将上述 URL 粘贴到浏览器的地址栏中，请求将不会返回任何内容。你仍然需要传递一些参数，这些参数将缩小请求的范围。对于 Mapbox Directions API，你需要为请求提供 **profile**（旅行模式）和 **coordinates**（原点和目标）：

- 在这种情况下，使用 `cycling` 为 profile，会生成自行车路线。
- 使用 `-84.518641, 39.134270` 作为起始坐标，`-84.512023, 39.102779` 作为目的地。请注意，这些坐标必须用分号 `;` 分隔。
- 使用可选参数 `geometries=geojson` 指定它以 GeoJSON 特性返回路线。

```
https://api.mapbox.com/directions/v5/mapbox/cycling/-84.518641,39.134270;-84.512023,39.102779?geometries=geojson
```

### 访问令牌

The only required item left is your access token. The access token is required to track the requests you make from your account _for this particular service_. You can create specific tokens for your requests or use your default token.

When adding this token, use an ampersand (the `&` symbol) before the token to append this to the request:

剩下的唯一必需项目是你的访问令牌。为了跟踪你账号 _针对此特定服务_ 发出的请求，需要访问令牌。你可以为请求创建特定令牌或使用默认令牌。

添加此令牌时，在令牌之前使用 `&` 符号，将此标记追加到请求中：

```
https://api.mapbox.com/directions/v5/mapbox/cycling/-84.518641,39.134270;-84.512023,39.102779?geometries=geojson&access_token={{ <UserAccessToken /> }}
```

现在你有一个请求，请将完整的 URL 粘贴到浏览器的地址栏中以获取响应。

## 查看响应

发出请求时，将返回 JSON 对象，并包含以下信息：

- **waypoints**：这是一个 _Waypoint_ 对象的数组。在这种情况下，此数组将包括起点和结束点。
- **routes**：这是按推荐等级降序排列的 _Route_ 对象的数组。在这种情况下，你没有请求其他路线，因此将只返回一条路线。您将在下一步中使用 `geometry` 属性在地图上显示此路线。
- **code**：此字符串表示响应的状态。在正常有效响应中，该值将为 `Ok`。

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

## 生成地图

现在，你已经了解了 Mapbox Directions API 请求和响应的工作原理，因此可以使用此 API 请求将路线添加到 Web 地图上。

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
// set the bounds of the map
var bounds = [[-123.069003, 45.395273], [-122.303707, 45.612333]];
map.setMaxBounds(bounds);

// initialize the map canvas to interact with later
var canvas = map.getCanvasContainer();

// an arbitrary start will always be the same
// only the end or destination will change
var start = [-122.662323, 45.523751];

// this is where the code for the next step will go
```


### 添加路由请求功能

接下来，你将构建一个名为 `getRoute` 的函数来发出 API 请求，并将获得的路线添加为新图层。然后，当地图加载时，调用该函数。

Within the `getRoute` function, specify the `start` and `end` coordinates. The start was defined outside of this function and the end will be passed in as an argument. Use an [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) object to make the API request. You can then use the response to get all the relevant objects and use the geometry to add the response as a layer to the map. You can end this part of the code by executing it with a request _after_ the map loads so that it makes a route that begins and ends at the start location.

Add the following code right after the start variable that you declared earlier:

```js
// create a function to make a directions request
function getRoute(end) {
  // make a directions request using cycling profile
  // an arbitrary start will always be the same
  // only the end or destination will change
  var start = [-122.662323, 45.523751];
  var url = 'https://api.mapbox.com/directions/v5/mapbox/cycling/' + start[0] + ',' + start[1] + ';' + end[0] + ',' + end[1] + '?steps=true&geometries=geojson&access_token=' + mapboxgl.accessToken;

  // make an XHR request https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
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
    // if the route already exists on the map, reset it using setData
    if (map.getSource('route')) {
      map.getSource('route').setData(geojson);
    } else { // otherwise, make a new request
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
    // add turn instructions here at the end
  };
  req.send();
}

map.on('load', function() {
  // make an initial directions request that
  // starts and ends at the same location
  getRoute(start);

  // Add starting point to the map
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
  // this is where the code from the next step will go
});
```

{{
  <Note title='Mapbox JavaScript SDK' imageComponent={<BookImage />}>
    <p>Mapbox also offers a JavaScript SDK, a node.js and browser JavaScript client, to interact with our web services directly in your web applications. You can use the JavaScript SDK to make the Directions API request directly. For more information on the Mapbox JavaScript SDK see the <a href="https://github.com/mapbox/mapbox-sdk-js/blob/master/docs/services.md">documentation on GitHub</a>.</p>
  </Note>
}}

Now that you've constructed the function that makes the requests and draws the routes, you'll want to load in an initial route from our starting point.

To see if this is working, open your browser's console (`Command+Alt+J` on a Mac, `Ctrl+Alt+J` on Windows) where you can interact with the application you've written so far. In the console, type `getRoute([-122.677738,45.522458])` to execute your function and pass in coordinates for a location in downtown Porland, OR. If everything is working, you should see a line drawn from the east side of the river to the west.

{{
  <DemoIframe src="/help/demos/directions-api/demo-one.html" />
}}

## Add your origin and destination

Now that you've created the start point (`getRoute(start)`) you'll provide a way to let the user select a destination. Add the next bit of code that allows the user to click the map and update the location of the destination:

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

## Add turn instructions

Because you added the `steps=true` parameter to the initial request, all the instructions for navigating the route are available to parse. Now add these steps to the sidebar in the div element called `instructions`.

```js
// get the sidebar and add the instructions
var instructions = document.getElementById('instructions');
var steps = data.legs[0].steps;

var tripInstructions = [];
for (var i = 0; i < steps.length; i++) {
  tripInstructions.push('<br><li>' + steps[i].maneuver.instruction) + '</li>';
  instructions.innerHTML = '<br><span class="duration">Trip duration: ' + Math.floor(data.duration / 60) + ' min 🚴 </span>' + tripInstructions;
}
```

In the directions response object, turn instructions are stored in the `routes` property. You can find `instructions` inside `routes` > `legs` > `steps` > `maneuver`. Each `instruction` is a string that describes what the bicycle rider should do next along a route.

Next, add some CSS to style the `div` so it appears on the left side of your map and has a white background.

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

## Finished product

You've used the Mapbox Directions API and Mapbox GL JS to add a bicycle route to a map.

{{
  <DemoIframe src="/help/demos/directions-api/index.html" />
}}

## Next steps

Now that you have practiced using the Mapbox Directions API, read about additional options in the [Directions API documentation](https://docs.mapbox.com/api/navigation/#directions). You can also try adding more details to your application:

- Style the origin and destination uniquely.
- Use the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) to assign the start and end points based on user input.
- Add more details, like distance and duration, to the turn instructions.
- Explore other ways to integrate directions services, including turn-by-turn instructions, into your applications including the [Mapbox GL directions plugin](https://github.com/mapbox/mapbox-gl-directions), the [JavaScript SDK](https://github.com/mapbox/mapbox-sdk-js#mapbox-sdk-js), and the Mapbox Navigation SDKs for [iOS](https://docs.mapbox.com/ios/navigation/overview/) and [Android](https://docs.mapbox.com/android/navigation/overview/).

Don't forget to explore other directions-related services like the [Mapbox Matrix API](https://docs.mapbox.com/api/navigation/#matrix) and [Optimization API](https://docs.mapbox.com/api/navigation/#optimization).



在"getRoute"函数中，指定"开始"和"结束"坐标。开始是在此函数之外定义的，结束将作为参数传入。使用 [XHR]（https：//开发人员.mozilla.org/en-US/文档/Web/API/XMLHttpRequest）对象发出 API 请求。然后，可以使用响应获取所有相关对象，并使用几何体将响应作为图层添加到地图中。可以通过加载映射加载的请求 [后] 来结束代码的这一部分，以便它创建在起始位置开始和结束的路由。

在之前声明的 start 变量之后添加以下代码：

{{
  [注意标题]'地图框 JavaScript SDK'图像组件_[书记/]
    <p>Mapbox 还提供 JavaScript SDK、node.js 和浏览器 JavaScript 客户端，可直接在 Web 应用程序中与我们的 Web 服务进行交互。您可以使用 JavaScript SDK 直接发出方向 API 请求。有关 Mapbox JavaScript SDK 的更多信息，请参阅 GitHub</a>.</p> 上的 [a href]https：//github.com/mapbox/mapbox-sdk-js/blob/master/docs/服务.md_文档
  </Note>
}}

现在，您已经构造了发出请求并绘制路由的函数，您需要从起点加载初始路由。

要查看这是否正常工作，请打开浏览器的控制台（Mac 上的"命令+Alt+J"，Windows 上的"Ctrl_Alt_J"），您可以在其中与到目前为止编写的应用程序进行交互。在控制台中，键入"getRoute（#122.677738，45.522458]）"以执行您的功能，并传递位于波尔兰市中心（OR）的坐标。如果一切工作，你应该看到一条线从河的东侧向西。

{{
  [演示框架 src]"/帮助/演示/方向-api/演示-一.html" /*
}}

• 添加您的始发地和目的地

现在，您已经创建了起点（"getRoute（开始"），您将提供一种允许用户选择目标的方法。添加允许用户单击地图并更新目标位置的下一个代码位：

{{
  [演示框架 src]"/帮助/演示/方向-api/演示-两个.html" /*
}}

• 添加转弯说明

由于将"步骤_true"参数添加到初始请求中，因此导航路由的所有说明都可以进行解析。现在，将这些步骤添加到称为"说明"的 div 元素中的侧边栏。

在方向响应对象中，转弯指令存储在"路线"属性中。您可以在"路线">"路线">"腿">"步">"机动"内找到"说明"。每个"指令"是一个字符串，描述自行车骑手下一步应该沿着路线做什么。

接下来，添加一些 CSS 以设置"div"的样式，使其显示在地图的左侧，并且具有白色背景。

• 成品

您已使用地图框方向 API 和 Mapbox GL JS 将自行车路线添加到地图中。

{{
  [演示框架 src]"/帮助/演示/方向-api/index.html" /*
}}

• 后续步骤

现在您已经练习了使用 Mapbox 方向 API，请阅读 [方向 API 文档]（https：//docs.mapbox.com/api/导航/#directions）中的其他选项。您还可以尝试向应用程序添加更多详细信息：

- 唯一地设置原点和目的地样式。
- 使用 [地图框地理编码 API]（https：//docs.mapbox.com/api/搜索/#geocoding）根据用户输入分配起点和终点。
- 向转弯说明添加更多详细信息，如距离和持续时间。
- 探索其他集成方向服务的方法，包括逐向说明， 到您的应用程序，包括 [Mapbox GL 方向插件]（https：//github.com/地图框-gl-方向），[JavaScript SDK]（https：//github.com/mapbox/mapbox/mapbox-js_mapbox-sdk 和 [iOS]的地图框导航 SDK（https：//docs.mapbox.com/ios/导航/概述/）和 [安卓]（https：//docs.mapbox.com/android/导航/概述/）。

不要忘记探索其他与方向相关的服务，如 [地图框矩阵 API]（https：//docs.mapbox.com/api/导航/#matrix）和 [优化 API]（https：//docs.mapbox.com/api/导航/#optimization）。
