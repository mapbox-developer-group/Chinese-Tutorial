 ---
title: 开始使用 Map Matching API
description: 使用 Map Matching API 创建一个允许用户定制行车路线的网页应用。
thumbnail: mapMatchingGetStartedDirections
topics:
- navigation
- directions
- web apps
level: 2
language:
- JavaScript
prereq: 熟悉前端开发技术.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
contentType: tutorial
---

大部分逐向导航应用假定用户希望通过最快路线到达目的地。但有时候相比于更快到达目的地，用户更想选择一条有趣或观光路线。例如：_用户在旧金山旅游。他们刚参观完海事博物馆，想去北滩吃批萨，希望沿途经过因拥有八个急转弯而被称为“世界上最弯曲街道”的九曲花街。_

经过九曲花街不是到达北滩的最快路线，但这条路线能提供最多的拍照机会！在大部分导航应用中，很难选出一条包含九曲花街的路线，因为这条路线并不是最便捷的。 这意味着用户会被导航到其他地方，无法满足他们想去九曲花街的需求。而 Mapbox 的 [Mapbox Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching) 可以让用户绘制自定义路线，能满足他们对不同路线的需求。

在这个教程中，你会创建一个允许用户定制自己旅游路线的网页应用，不考虑定制路线是否是最高效的。应用用户会在地图上用 **Mapbox GL Draw plugin** 的画图工具绘制自己的路线，然后应用将绘制的坐标发送给 **Map Matching API** 生成新行车路线的逐向导航。

{{
  <DemoIframe src="/help/demos/get-started-map-matching-api/index.html" />
}}

{{<Note title="The Map Matching API vs. the Directions API" imageComponent={<BookImage />}>}}

Mapbox Map Matching API 很像 [Directions API](https://docs.mapbox.com/api/navigation/#directions)。Mapbox Map Matching API 可以生成路线，路线时长，以及导航，和 Direction API 一样。但是 Direction API 生成_优化_过的路线，而 Map Matching API 会在 OpenStreetMap 路网上生成最接近请求坐标的路线。 

{{</Note>}}

## 开始
为了完成教程，你需要：

- **一个 Mapbox access token。** 你的 Mapbox access tokens 可以在[账户](https://account.mapbox.com/)页面找到。
- **Mapbox GL JS。** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) 是一个用来构建网页地图的 JavaScript API。
- **Mapbox GL Draw plugin.** [Mapbox GL Draw plugin](https://github.com/mapbox/mapbox-gl-draw) 用于在 Mapbox GL JS 创建的地图上添加绘制和编辑功能。
- **Mapbox Map Matching API.** [Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching) 将坐标嵌入 OpenStreetMap 路网，并返回路线产生的导航信息。 
- **jQuery.** [jQuery](https://jquery.com/) 是用来给应用添加 API 请求的库。
- **编辑器。** 自选一款可以编辑 HTML，CSS 和 JavaScript 的编辑器。

## 创建地图
开始编写应用，首先使用 [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) 创建地图。

打开编辑器创建文件 `index.html`，粘贴下方代码到编辑器。这些代码创建了页面结构，并导入 Mapbox GL JS 和 jQuery 到页面的 `<head>`。Mapbox GL JS 的 JavaScript 和 CSS 文件让你能够使用 Mapbox GL JS 功能和样式，jQuery 使你能通过 [Ajax](https://api.jquery.com/jquery.ajax/) 解析 Map Matching API 调用。

在 `<body>` 的中有一个 ID 为 `map` 的 `<div>` 元素，包含页面中显示地图的容器。

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Map Matching API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- 导入 Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- 导入 jQuery -->
  <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>

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
  <!-- 创建地图容器 -->
  <div id='map'></div>

  <script>
    // 添加你的 Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // 指定容器 ID 
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-122.42136449,37.80176523], // 指定中心点 
      zoom: 14.5, // 指定初始缩放等级
    });
  </script>
</body>

</html>
```

上述代码设置了地图样式，地图中心点和缩放等级。

保存修改。在浏览器打开 HTML 文件会看到渲染出的地图，中心点为旧金山。

## 添加绘制工具

{{<Note title="Options for passing coordinates to the Map Matching API" imageComponent={<BookImage />}>}}

在这个教程的应用里，Map Matching API 使用用户通过 Mapbox GL Draw 工具直接在地图上添加的点生成路线。不过开发者通常希望通过代码添加 Map Matching API 所需的点。例如，Map matching API 可以访问包含地标坐标的数据集来创建风光游览路线，还可以访问有导航终点车库位置信息的数据集。

{{</Note>}}

[Mapbox GL Draw plugin](https://github.com/mapbox/mapbox-gl-draw) 支持在 Mapbox GL JS 创建的地图上添加绘制功能。在这一节，你会添加 Mapbox GL Draw 的 `line_tool` 和 `trash` 工具到应用里，它们允许用户绘制线，以及删除线。首先，添加 Mapbox GL Draw plugin 的 JavaScript 和 CSS 链接到 HTML 文件 head 里：

```html
<script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.js'></script>
<link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.css' type='text/css' />
```

链接添加后，你就能在应用中使用 Draw 插件。添加 Draw 插件时，你可以指定用户使用绘制工具在地图上绘制的线条样式。在 `</script>` 闭合标签上方位置添加以下代码。

```js
var draw = new MapboxDraw({
  // 不显示所有地图工具，只显示画线工具和删除工具
  displayControlsDefault: false,
  controls: {
    line_string: true,
    trash: true
  },
  styles: [
    // 设置用户输入坐标线条样式
    {
      "id": "gl-draw-line",
      "type": "line",
      "filter": ["all", ["==", "$type", "LineString"],
        ["!=", "mode", "static"]
      ],
      "layout": {
        "line-cap": "round",
        "line-join": "round"
      },
      "paint": {
        "line-color": "#438EE4",
        "line-dasharray": [0.2, 2],
        "line-width": 4,
        "line-opacity": 0.7
      }
    },
    // 设置 halos 顶点样式
    {
      "id": "gl-draw-polygon-and-line-vertex-halo-active",
      "type": "circle",
      "filter": ["all", ["==", "meta", "vertex"],
        ["==", "$type", "Point"],
        ["!=", "mode", "static"]
      ],
      "paint": {
        "circle-radius": 12,
        "circle-color": "#FFF"
      }
    },
    // 设置顶点样式
    {
      "id": "gl-draw-polygon-and-line-vertex-active",
      "type": "circle",
      "filter": ["all", ["==", "meta", "vertex"],
        ["==", "$type", "Point"],
        ["!=", "mode", "static"]
      ],
      "paint": {
        "circle-radius": 8,
        "circle-color": "#438EE4",
      }
    },
  ]
});

// 给地图添加绘制工具
map.addControl(draw);
```

保存文件刷新页面。你会看到设定的 Draw 插件控制，`line_tool` 和 `delete` 图标出现在页面右边。点击 `line_tool` 图标。在地图上点击一下开始绘制路径，再点击一次或多次来绘制路线。当你完成绘制时，在终点点击一次结束路径。地图会用蓝色虚线来表示你绘制的路径。关于更多线条样式的信息可以阅读 Mapbox GL Draw 文档的[绘制样式](https://github.com/mapbox/mapbox-gl-draw/blob/master/docs/API.md#styling-draw)一节。

在接下来到步骤中，你会将本节的代码与获取绘制路径，收集坐标来使用 Map Matching API 的函数关联起来。

{{
<AppropriateImage imageId="mapMatchingGetStartedDrawTools" alt="Screenshot showing the Mapbox GL Draw plugin tools added to the right side of the map." />
}}

## 添加侧边栏

给网页应用添加侧边栏，显示如何使用应用的说明。侧边栏也会作为显示逐向导航的地方，你会在后边的步骤里设置。

在 HTML 的 `<body>` 里添加新 `<div>`。`<div>` 会包含应用说明，以及后续的逐向导航。

```html
<div class="info-box">
  <div id="info">
    <p>在右边使用绘制工具绘制路线。为了得到最佳路线匹配，请每隔一定距离画点。</p>
  </div>
  <div id="directions"></div>
</div>
```

添加下边的 CSS 到 HTML `<style>` 部分，设置新 `<div>` 样式：

```css
.info-box {
  position: absolute;
  margin: 20px;
  width: 25%;
  top: 0;
  bottom: 40%;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.9);
  overflow-y: scroll;
  font-family: sans-serif;
  font-size: 0.8em;
  line-height: 2em;
}

#info {
  font-size: 16px;
  font-weight: bold;
}
```

保存文件并刷新页面。新说明框会显示在页面左侧。 

{{
<AppropriateImage imageId="mapMatchingGetStartedSidebar" alt="Screenshot showing a sidebar added to the map." />
}}

## 添加 Map Matching API

Map Matching API 要求提供两个参数：查询应该使用的 `profile` 和要在 OpenStreetMap 路网中匹配的坐标 `coordinates`。`profile` 可以是 `walking`，`cycling`，`driving` 或 `driving-traffic` 中的一种。坐标是按顺序以分号隔开的 `{longitude},{latitude}` 坐标对，可以包含 2 到 100 个坐标。

```
https://api.mapbox.com/matching/v5/mapbox/{profile}/{coordinates}.json?access_token=YOUR_MAPBOX_ACCESS_TOKEN
```

Map Matching API 也接收几个自定义查询的可选参数。对于本应用，你需要两个可选参数：

- `radiuses`：分号隔开的列表，说明为了和路网匹配坐标可以被移动的最大距离。添加半径告诉 Map Matching API 必须和用户输入坐标匹配到的精确程度，用户坐标可能在 OpenStreetMap 路网上无法匹配已有位置。半径数量必须和请求坐标数量一致。
- `steps`: 设置为 `true` 返回逐向导航。

如果想了解更多 Map Matching API 及其参数，可以浏览 [Map Matching API 文档](https://docs.mapbox.com/api/navigation/#map-matching)。

下边的查询样例使用 `driving` 配置，有两个坐标对和两个 `radiuses`，设置 `steps` 为 `true`：

```
https://api.mapbox.com/matching/v5/mapbox/driving/-117.17282,32.71204;-117.17288,32.71225?steps=true&radiuses=25;25&access_token={{ <UserAccessToken /> }}
```

使用 `radiuses` 和 `steps` 参数的 Map Matching API 请求返回包含 `matchings` 返回值，match 对象数组。match 对象包含路线段 route leg 对象，提供关于路线段的详细信息，包括逐向导航。你会使用 Map Matching API 返回信息做两件事情：将匹配路线绘制到地图上，以及返回逐向导航。

为了使用 Map Matching API，你要写两个函数，`updateRoute` 和 `getMatch`。`updateRoute` 使用用户绘制线产生的坐标，并格式化后用于 Map Matching API 查询。`getMatch` 构建查询字串，并使用 Ajax 请求 Map Matching API。两者结合使用就会用绘制到地图上的坐标发起 API 请求，并返回完成剩下应用所需的数据。添加以下代码到 `</script>` 闭合标签上方：

```js
// 使用绘制的坐标发起 Map Matching API 请求
function updateRoute() {
  // 设置 profile
  var profile = "driving";
  // 获取绘制到地图的坐标
  var data = draw.getAll();
  var lastFeature = data.features.length - 1;
  var coords = data.features[lastFeature].geometry.coordinates;
  // 格式化坐标
  var newCoords = coords.join(';')
  // 设置每个坐标匹配半径为 25 米
  var radius = [];
  coords.forEach(element => {
    radius.push(25);
  });
  getMatch(newCoords, radius, profile);
}

// 发起 Map Matching 请求
function getMatch(coordinates, radius, profile) {
  // 用分号连接起半径数据
  var radiuses = radius.join(';')
  // 创建查询
  var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;

  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    // 从返回值中获取坐标
    var coords = data.matchings[0].geometry;
    console.log(coords);
    // 后续步骤代码
  });
}
```

通过在 `updateRoute` 中调用 `getMatch` 函数，你可以访问用户绘制坐标，并在 Map Matching API 请求中使用它们。在下一步中，你会添加新的线条显示匹配路线，但是现在你可以通过 `console.log()` 查看它们。

为了在用户绘制或更新地图线条时调用 `getMatch`，添加以下代码在 `</script>` 闭合标签前：

```js
map.on('draw.create', updateRoute);
map.on('draw.update', updateRoute);
```

保存文件，刷新页面并打开开发者工具。当你在地图上画线时，应用会打印出 Map Matching API 返回的坐标到 JavaScript 控制台。

{{
<AppropriateImage imageId="mapMatchingGetStartedConsole" alt="Screenshot showing the returned coordinates displayed in a browser's JavaScript console." />
}}

## 绘制 Map Matching 路线
接下来，你会创建 `addRoute` 函数，利用 Map Matching API 返回的坐标，通过新图层添加到地图上。在 `</script>` 闭合标签上添加以下代码：

```js
// 在地图上将 Map Matching 路线绘制为新图层
function addRoute(coords) {
  // 如果有已经载入的路线，先删除掉它
  if (map.getSource('route')) {
    map.removeLayer('route')
    map.removeSource('route')
  } else { // 给地图添加新图层
    map.addLayer({
      "id": "route",
      "type": "line",
      "source": {
        "type": "geojson",
        "data": {
          "type": "Feature",
          "properties": {},
          "geometry": coords
        }
      },
      "layout": {
        "line-join": "round",
        "line-cap": "round"
      },
      "paint": {
        "line-color": "#03AA46",
        "line-width": 8,
        "line-opacity": 0.8
      }
    });
  };
}
```

在 `getRoute` 函数中调用 `addRoute` 以使用 Map Matching API 返回值。getRoute 现在如下所示：

```js
// 发起 Map Matching 请求
function getMatch(coordinates, radius, profile) {
  // 用分号连接起半径数据
  var radiuses = radius.join(';')
  // 创建查询
  var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;
  console.log(query)
  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    // 从返回值中获取坐标
    var coords = data.matchings[0].geometry;
    // 在地图上绘制路线
    addRoute(coords);
  });
}
```

保存文件，刷新页面。当你用 `line_draw` 工具画路线时，生成的路线也会显示在地图上。正如你所看到的，用户绘制的线不总是和 Map Matching API 生成的路线匹配。这是由于 Map Matching API 使用用户提供的坐标时，部分坐标可能无法直接在路网上定位到，这种情况下 Map Matching API 根据你在 `radiuses` 参数中指定的 25 米半径计算最近路线坐标。

{{
<AppropriateImage imageId="mapMatchingGetStartedNewLayer" alt="Screenshot showing the coordinates returned by the Map Matching API as a new layer on the map." />
}}

## 显示逐向导航
现在可以添加 Map Matching API 的逐向导航到侧边栏了！为了实现这个功能，我们需要写一个新函数 `getInstructions`，这要求你深入 Map Matching API 返回值对象中获取所需信息：路线全程时长，路线每一步的行车指令。（浏览Map Matching API 文档(https://docs.mapbox.com/api/navigation/#route-step-object)了解更多关于 Map Matching API 逐向路线对象返回值的信息。）在 `getMatch` 方法下添加以下代码：

```js
function getInstructions(data) {
  // 获取添加导航的侧边栏
  var directions = document.getElementById('directions');

  var legs = data.legs;
  var tripDirections = [];
  // 在返回对象中输出每个路线段导航指令
  for (var i = 0; i < legs.length; i++) {
    var steps = legs[i].steps;
    for (var j = 0; j < steps.length; j++) {
      tripDirections.push('<br><li>' + steps[j].maneuver.instruction) + '</li>';
    }
  }
  directions.innerHTML = '<br><h2>Trip duration: ' + Math.floor(data.duration / 60) + ' min.</h2>' + tripDirections;
}
```

下一步，在 `getRoute` 函数中调用 `getInstructions` 以使用 Map Matching API 返回值。`getRoute` 现在如下所示：

```js
// 发起 Map Matching 请求
function getMatch(coordinates, radius, profile) {
  // 用分号连接起半径数据
  var radiuses = radius.join(';')
  // 创建查询
  var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;
  console.log(query)
  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    var coords = data.matchings[0].geometry;
    // 在地图上绘制路线
    addRoute(coords);
    getInstructions(data.matchings[0]);
  });
}
```

保存文件，刷新页面。当你在地图上画线时，你会在侧边栏看到路线时长和逐向导航指令。

{{
<AppropriateImage imageId="mapMatchingGetStartedDirections" alt="Screenshot showing turn-by-turn directions displayed in the sidebar of the map." />
}}

## 允许用户删除路线
最后一步，添加允许用户删除他们绘制在地图上的路线。 

```js
// 如果用户点击删除按钮，移除已存在的图层
function removeRoute() {
  if (map.getSource('route')) {
    map.removeLayer('route');
    map.removeSource('route');
  } else {
    return;
  }
}
```

添加以下代码，将 `removeRoute` 与插件的删除按钮关联起来：

```js
  map.on('draw.delete', removeRoute);
```

保存文件，刷新页面。当你画条线，然后点击 Draw 插件的删除按钮后，路线会被移除页面。

## 最终产品

你已经创建了一个使用 Mapbox Map Matching API 将用户自定义坐标嵌入路网的应用。同时可以在地图上显示路线，并为用户提供逐向导航。

{{
  <DemoIframe src="/help/demos/get-started-map-matching-api/index.html" />
}}

最终的 HTML 文件如下所示：

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>开始使用地图匹配 API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- 导入 Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- 导入 jQuery -->
  <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>
  <!-- 导入 Mapbox GL Draw -->
  <script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.js'></script>
  <link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.css' type='text/css' />

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

    .info-box {
      position: absolute;
      margin: 20px;
      width: 25%;
      top: 0;
      bottom: 40%;
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.9);
      overflow-y: scroll;
      font-family: sans-serif;
      font-size: 0.8em;
      line-height: 2em;
    }

    #info {
      font-size: 16px;
      font-weight: bold;
    }
  </style>
</head>

<body>
  <!-- 创建地图容器 -->
  <div id='map'></div>

  <div class="info-box">
    <div id="info">
      <p>在右边使用绘制工具绘制路线。为了得到最佳路线匹配，请每隔一定距离画点。</p>
    </div>
    <div id="directions"></div>
  </div>

  <script>
    // 添加你的 Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken/> }}';
    var map = new mapboxgl.Map({
      container: 'map', // 指定容器 ID 
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-122.42136449,37.80176523], // 指定起始中心点
      zoom: 14.5, // 指定初始缩放等级
    });

    var draw = new MapboxDraw({
      // 不显示所有地图工具，只显示画线工具和删除工具
      displayControlsDefault: false,
      controls: {
        line_string: true,
        trash: true
      },
      styles: [
        // 设置用户输入坐标线条样式
        {
          "id": "gl-draw-line",
          "type": "line",
          "filter": ["all", ["==", "$type", "LineString"],
            ["!=", "mode", "static"]
          ],
          "layout": {
            "line-cap": "round",
            "line-join": "round"
          },
          "paint": {
            "line-color": "#438EE4",
            "line-dasharray": [0.2, 2],
            "line-width": 4,
            "line-opacity": 0.7
          }
        },
        // 设置 halos 顶点样式
        {
          "id": "gl-draw-polygon-and-line-vertex-halo-active",
          "type": "circle",
          "filter": ["all", ["==", "meta", "vertex"],
            ["==", "$type", "Point"],
            ["!=", "mode", "static"]
          ],
          "paint": {
            "circle-radius": 12,
            "circle-color": "#FFF"
          }
        },
        // 设置顶点样式
        {
          "id": "gl-draw-polygon-and-line-vertex-active",
          "type": "circle",
          "filter": ["all", ["==", "meta", "vertex"],
            ["==", "$type", "Point"],
            ["!=", "mode", "static"]
          ],
          "paint": {
            "circle-radius": 8,
            "circle-color": "#438EE4",
          }
        },
      ]
    });

    // 给地图添加绘制工具
    map.addControl(draw);

    function updateRoute() {
      // 设置 profile
      var profile = "driving";
      // 获取绘制到地图的坐标
      var data = draw.getAll();
      var lastFeature = data.features.length - 1;
      var coords = data.features[lastFeature].geometry.coordinates;
      // 格式化坐标
      var newCoords = coords.join(';')
      // 设置每个坐标匹配半径为 25 米
      var radius = [];
      coords.forEach(element => {
        radius.push(25);
      });
      getMatch(newCoords, radius, profile);
    }

    // 发起 Map Matching 请求
    function getMatch(coordinates, radius, profile) {
      // 获取绘制到地图的坐标
      var radiuses = radius.join(';')
      // 创建查询
      var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;

      $.ajax({
        method: 'GET',
        url: query
      }).done(function(data) {
        // 从返回值中获取坐标
        var coords = data.matchings[0].geometry;
        // 绘制路线到地图
        addRoute(coords);
        getInstructions(data.matchings[0]);
      });
    }

    // 在地图上将 Map Matching 路线绘制为新图层
    function addRoute(coords) {
      // 如果有已经载入的路线，先删除掉它
      if (map.getSource('route')) {
        map.removeLayer('route')
        map.removeSource('route')
      } else {
        map.addLayer({
          "id": "route",
          "type": "line",
          "source": {
            "type": "geojson",
            "data": {
              "type": "Feature",
              "properties": {},
              "geometry": coords
            }
          },
          "layout": {
            "line-join": "round",
            "line-cap": "round"
          },
          "paint": {
            "line-color": "#03AA46",
            "line-width": 8,
            "line-opacity": 0.8
          }
        });
      };
    }

    function getInstructions(data) {
      // 获取添加导航的侧边栏
      var directions = document.getElementById('directions');

      var legs = data.legs;
      var tripDirections = [];
      // 在返回对象中输出每个路线段导航指令
      for (var i = 0; i < legs.length; i++) {
        var steps = legs[i].steps;
        for (var j = 0; j < steps.length; j++) {
          tripDirections.push('<br><li>' + steps[j].maneuver.instruction) + '</li>';
        }
      }
      directions.innerHTML = '<br><h2>Trip duration: ' + Math.floor(data.duration / 60) + ' min.</h2>' + tripDirections;
    }

    // 如果用户点击删除按钮，移除已存在的图层
    function removeRoute() {
      if (map.getSource('route')) {
        map.removeLayer('route');
        map.removeSource('route');
      } else {
        return;
      }
    }

    map.on('draw.create', updateRoute);
    map.on('draw.update', updateRoute);
    map.on('draw.delete', removeRoute);
  </script>
</body>

</html>

```

## 下一步
想基于本教程使用的工具和技术开发产品，查阅以下资料：
- 在 [Map Matching API 文档](https://docs.mapbox.com/api/navigation/#map-matching)中学习如何利用可选参数控制响应结果中的返回内容。
- 在 [添加 GeoJSON 线示例](https://docs.mapbox.com/mapbox-gl-js/example/geojson-line/)和 [`addLayer` 文档](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer)中了解更多关于如何用 Mapbox GL JS 给地图添加新图层的知识。
- Learn more about how to use the Mapbox GL Draw plugin in the [Show drawn polygon area example](https://docs.mapbox.com/mapbox-gl-js/example/mapbox-gl-draw/) and in the [Mapbox GL Draw plugin documentation](https://github.com/mapbox/mapbox-gl-draw/tree/master/docs).
- 在[显示绘制的多边形区域示例](https://docs.mapbox.com/mapbox-gl-js/example/mapbox-gl-draw/)和 [Mapbox GL Draw plugin](https://github.com/mapbox/mapbox-gl-draw/tree/master/docs) 文档里了解更多关于如何使用 Mapbox GL Draw 插件的知识。
