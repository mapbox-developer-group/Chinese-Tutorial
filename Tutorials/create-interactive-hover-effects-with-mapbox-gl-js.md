---
title: 使用 Mapbox GL JS 创建交互式悬停效果
description: 结合 Mapbox GL JS 使用 feature state 和 expressions 来动态赋予一张地图上各要素不同的样式。该地图可视化了过去一周发生的地震。
thumbnail: featureStateFinal
topics:
- web apps
level: 2
language:
- JavaScript
prereq: 熟悉前端开发概念。
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
<!--copyeditor ignore magnitude -->
在本教程中，你会创建一张展示过去一周发生的地震位置分布的地图。你会使用 [expressions](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions) 来根据地震强度设定地震要素的样式。最后，你会使用 [feature state](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions-feature-state) 在用户的鼠标移至要素时赋予地震要素这些样式，并在用户鼠标移开后移除它们。

{{
  <DemoIframe src="/help/demos/create-interactive-hover-effects-with-mapbox-gl-js/index.html" />
}}

Feature state 是一组用户自定义的属性集合。这些属性能够被动态地赋予地图上的某要素。Feature State 会与 [expressions](https://docs.mapbox.com/help/glossary/expression/) 结合使用，来赋予在数据集或切片集中的矢量或 GeoJSON 数据源的 [features](https://www.mapbox.com/help/define-features/) 样式。每个在数据源中的要素都必须有一个唯一的数字 `id`，以使得 feature state 能够正确使用。正如你将会在本教程中所要学习的，如果你在运行时添加一个 GeoJSON 数据源，你可以使用在 [`map.addSource()`](https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource) 的 `generateId` 选项来给每一个要素添加一个 `id`。对于在运行时前被加入的矢量数据源或 GeoJSON 数据源，你必须在数据源被添加到地图前给每一个要素设定一个唯一的 `id`。

你可以将 feature state 理解为一个打开或关闭风扇的开关。你会使用 feature state 来定义这个开关是什么，并使用 expressions 来设定样式。在本例中，触发事件是一个用户将鼠标移至或移开某一要素。这会根据 expressions 设定的规则来更新要素的样式。

<!--copyeditor ignore magnitude -->
Feature state 使你能够根据用户交互行为来更新地图图层中的各要素的样式，而无需在每次交互事件发生后重新渲染根本的几何属性的数值。在本教程中，feature state触发事件将会是一个用户将鼠标悬停于一个地震要素之上。而你将会使用 feature state 来根据地震强度大小来更新该要素的半径大小及颜色。

## 开始入门
为了完成本教程，你会使用到：
<!--copyeditor ignore magnitude -->
- **A Mapbox access token。** 你的 Mapbox access tokens 在你的 [用户主页](https://account.mapbox.com/) 中。
- **Mapbox GL JS。** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) 是一个用于创建网页地图的 JavaScript API。
- **A text editor。** 使用你喜爱的文本编辑器来编写 HTML，CSS 和 Javascript。
- **The USGS Earthquake Catalog API。** 你会使用 [USGS Earthquake Catalog API](https://earthquake.usgs.gov/fdsnws/event/1/) 来获取过去一周内发生的一次或多次地震的信息。

## 创建地图
开始时，你会使用 [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) 创建一张地图。打开你的文本编辑器并新建一个名为 `index.html` 的文件。将一下的代码输入你的文本编辑器中，来修改这个新建的 HTML 文件：

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Create interactive hover effects with Mapbox GL JS</title>
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
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.44121, 37.76132], // Specify the starting position [lng, lat]
      zoom: 3.5 // Specify the starting zoom
    });
  </script>
  
</body>
</html>        
```

这段代码创建了页面的结构。它在页面的 `<head>` 导入了 Mapbox GL JS，使得你能够在你的网页程序中使用 Mapbox GL JS 的功能和样式。

这段代码在页面的 `<body>` 中包含一个拥有 `map` ID 的 `<div>` 元素。`<div>` 是在页面上地图被显示所在的容器。


保存你的更改。在浏览器中打开这个 HTML 文档来看下渲染的地图，它的中心位于美国西部。

{{
<AppropriateImage imageId="featureStateBaseMap" alt="Basemap using the Mapbox Outdoors style" />
}}

## 添加侧边栏
<!--copyeditor ignore magnitude -->
在你的 HTML 的 `<body>` 中，添加一个新的 `<div>`。这个 `<div>` 会被用于显示各地震的强度，位置以及发生的时间：

```html
<div class='quakeInfo'>
  <div><strong>Magnitude:</strong>&nbsp;<span id='mag'></span></div>
  <div><strong>Location:</strong>&nbsp;<span id='loc'></span></div>
  <div><strong>Date:</strong>&nbsp;<span id='date'></span></div>
</div>
```

为了赋予这个新 `<div>` 样式，需添加一下 CSS 至你的 HTML 的 `<style>` 部分：

```css
.quakeInfo {
  position: absolute;
  font-family: sans-serif;
  margin-top: 5px;
  margin-left: 5px;
  padding: 5px;
  width: 30%;
  border: 2px solid black;
  font-size: 14px;
  color: #222;
  background-color: #fff;
  border-radius: 3px;
}
```

最后，添加3个新变量。你会使用它们来指向新的使用它们 ID 的 `<span>`。添加以下代码到你的 Javascript 中结束的 `</script>` 的标签上方：

```js
var magDisplay = document.getElementById('mag');
var locDisplay = document.getElementById('loc');
var dateDisplay = document.getElementById('date');
```
<!--copyeditor ignore magnitude -->
保存你的修改并刷新页面。新的侧边狼会被显示在页面的左部。在下面的步骤中，你会使用你创建的 `<span>` 在侧边栏中显示地震的强度，位置和时间。

{{
<AppropriateImage imageId="featureStateSidebar" alt="Basemap using the Mapbox Outdoors style, with a styled sidebar with the words Magnitude, Location, and Date" />
}}

## 添加地震数据源
<!--copyeditor ignore magnitude -->
Mapbox GL JS [`addSource` 实例](https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource) 使你能够添加一个新的数据源到地图上。在本例中，你会使用来自 [USGS Earthquake Catalog API](https://earthquake.usgs.gov/fdsnws/event/1/) 的数据。它会返回最近发生的地震的信息，包括强度，位置以及发生的时间。

Earthquake Catalog API 默认返回过去30天所有事件。但对于这个网页程序，你则会利用可选择的 `starttime` 参数返回过去7天的所有事件。你会使用 [JavaScript `Date` constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) 来获取 [ISO 8601 timestamp](https://www.iso.org/iso-8601-date-and-time-format.html) 形式的7天前的日期。这也正是 USGS Earthquake Catalog API 所要求的。
将以下 Javascript 代码添加至你的文档中：
```js
var today = new Date();
// Use JavaScript to get the date a week ago
var priorDate = new Date().setDate(today.getDate() - 7);
// Set that to an ISO8601 timestamp as required by the USGS earthquake API
var priorDateTs = new Date(priorDate);
var sevenDaysAgo = priorDateTs.toISOString();
```   

你会在访问 Earthquake Catalog API 时使用 `sevenDaysAgo` 这个变量。（如果你使用的是如 [Moment.js](https://momentjs.com/)  JavaScript 日期处理类库，将当前日期减去7天会使用更少的步骤。但由于本教程的需求，这些步骤是用纯原生 Javascript 显示的。）

对于本网页程序，你会使用 Earthquake Catalog API 的可选  `format` 参数以返回 GeoJSON 格式的数据。你同时也会利用可选参数 `eventtype` 和 `minmagnitude` 来限制查询结果为1级以上的地震。

通过调整这些可选参数，USGS Earthquake Catalog API 查询语句为：
```
"https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&eventtype=earthquake&minmagnitude=1&starttime=" + sevenDaysAgo
```

为了将向 Earthquake Catalog API 访问查询得到的结果作为一个数据源添加至你的程序中，你会将 `addSource` 嵌入在 `map.on('load')` 函数中，以使得新的数据源在地图被渲染前不会被导入。将下列代码添加至你的 Javacript 代码中：
 

```js
map.on('load', function() {

  map.addSource('earthquakes', {
    'type': 'geojson',
    'data': 'https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&eventtype=earthquake&minmagnitude=1&starttime=' + sevenDaysAgo,
    'generateId': true // This ensures that all features have unique IDs
  });
  
});  
```

{{<Note title="Setting unique IDs for features" imageComponent={<BookImage />}>}}
Feature state 要求每一个要素有一个在数据源或数据源图层中唯一的 `id`。 

正如本教程中的 Earthquake Catalog API，如果你正在使用一个在运行时生成的 GeoJSON 数据源，你可以通过设置 `map.addSource()` 中的 `generateId` 属性为 `true` 来为每一个要素添加一个 `id`。这个会根据要素在数据源中的索引来为每一个新数据源中的要素生成一个 `id` 。

`generateId` 方法不仅适合于在运行时被添加的 GeoJSON 数据源。对于切片集来说，或对于在运行时前被添加的 GeoJSON 数据源来说，在数据源被添加至地图前，每一个要素都必须赋予唯一的 `id`。
{{</Note>}}

在下一步中，你会添加一个使用数据源 `earthquakes` 的样式图层至地图中。

## 添加地震图层
Mapbox GL JS [`addLayer` 实例](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer) 创建一个新的地图图层，其定义了来自某一特定数据源的数据样式。在本例中，数据来自于你在上一步中创建的 `earthquakes` 数据源。

将以下 `addLayer` 功能添加到 `map.on('load')` 中的你在上一步所写的 `addSource` 函数下方。

```js
map.addLayer({
  'id': 'earthquakes-viz',
  'type': 'circle',
  'source': 'earthquakes',
  'paint': {
    'circle-stroke-color': '#000',
    'circle-stroke-width': 1,
    'circle-color': '#000'
  }
});
```
<!--copyeditor ignore magnitude -->
保存你的修改并在浏览器中刷新页面。你会看到正如在 `paint` 属性所声明的一样，新的 `earthquake-viz` 图层以黑点的形式绘制各地震点。在下一步中，你会用到：
- **`feature-state`** 来修改当用户鼠标悬停于某独立要素之上时它的样式
- **`interpolate`, `linear`, 和 `get` expressions** 来根据地震震级大小来确定新的样式

{{
<AppropriateImage imageId="featureStateAddLayer" alt="Basemap with black circles representing the features in the new earthquake-viz layer" />
}}

## 使用 feature state 赋予地震样式
Feature state 能够被用来利用任何支持 [data-driven styling](https://docs.mapbox.com/help/glossary/data-driven-styling/) 的绘画属性样式的值来赋予它们样式。在 [Mapbox style specification](https://www.mapbox.com/mapbox-gl-js/style-spec/#layers) 中能了解更多关于绘画属性支持层级。在 feature state 中，要素可根据它们的 `id` 属性被识别。这些属性必须是在数据源或数据源图层中独一无二的。当你使用 `addSource` 来添加地震数据为数据源时，你会设置 `'generateId': true`，这会确保所有的要素都有唯一的ID。

在本例中，你会使用 feature state 来根据一个有布尔值的属性 (`hover`) 来改变代表要素的圆的颜色和半径大小。然后你会利用 [`setFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate) 来定义 `hover` 属性。
<!--copyeditor ignore magnitude -->
更新 `addLayer` 来为 `circle-radius` 和 `circle-color`使用 feature state。更新的代码也使用 expressions [`interpolate` operator](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions-interpolate) 来依据选中的地震要素的震级来设置 `circle-radius` 和 `circle-color` 。

```js
map.addLayer({
  'id': 'earthquakes-viz',
  'type': 'circle',
  'source': 'earthquakes',
  'paint': {
    // The feature-state dependent circle-radius expression will render
    // the radius size according to its magnitude when
    // a feature's hover state is set to true
    'circle-radius': [
      'case',
      ['boolean',
        ['feature-state', 'hover'],
        false
      ],
      [
        'interpolate', ['linear'],
        ['get', 'mag'],
        1, 8,
        1.5, 10,
        2, 12,
        2.5, 14,
        3, 16,
        3.5, 18,
        4.5, 20,
        6.5, 22,
        8.5, 24,
        10.5, 26
      ],
      5
    ],
    'circle-stroke-color': '#000',
    'circle-stroke-width': 1,
    // The feature-state dependent circle-color expression will render
    // the color according to its magnitude when
    // a feature's hover state is set to true
    'circle-color': [
      'case',
      ['boolean',
        ['feature-state', 'hover'],
        false
      ],
      [
        'interpolate', ['linear'],
        ['get', 'mag'],
        1, '#fff7ec',
        1.5, '#fee8c8',
        2, '#fdd49e',
        2.5, '#fdbb84',
        3, '#fc8d59',
        3.5, '#ef6548',
        4.5, '#d7301f',
        6.5, '#b30000',
        8.5, '#7f0000',
        10.5, '#000'
      ],
      '#000'
    ]
  }
});
```

## 定义悬停属性
接下来，你会用 [`setFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate) 来定义 `hover` 属性。为了触发当用户将鼠标移至某一地震要素时 feature state 的改变事件，你会将 `setFeatureState` 嵌入到 `map.on('mousemove')` 函数中。

以下代码创建了几个新变量，每一个变量都会因每一个 `map.on('mousemove')` 事件而被更新：
<!--copyeditor ignore magnitude -->
- `quakeID`: 这个变量会被设置为当前要素的 `id` ，使你能够指向单独的每一个地震。
- `quakeMagnitude`: 返回的当前要素的震级。
- `quakeLocation`: 返回的当前要素的位置。
- `quakeDate`: 返回的当前要素的日期。

粘贴以下代码至你的 Javacript 代码中，于最后的 `</script>` 标签上方。

```js
var quakeID = null;

map.on('mousemove', 'earthquakes-viz', (e) => {

  map.getCanvas().style.cursor = 'pointer';
  // Set variables equal to the current feature's magnitude, location, and time
  var quakeMagnitude = e.features[0].properties.mag;
  var quakeLocation = e.features[0].properties.place;
  var quakeDate = new Date(e.features[0].properties.time);

  // Check whether features exist
  if (e.features.length > 0) {
    // Display the magnitude, location, and time in the sidebar
    magDisplay.textContent = quakeMagnitude;
    locDisplay.textContent = quakeLocation;
    dateDisplay.textContent = quakeDate;

    // If quakeID for the hovered feature is not null,
    // use removeFeatureState to reset to the default behavior
    if (quakeID) {
      map.removeFeatureState({
        source: "earthquakes",
        id: quakeID
      });
    }

    quakeID = e.features[0].id;

    // When the mouse moves over the earthquakes-viz layer, update the
    // feature state for the feature under the mouse
    map.setFeatureState({
      source: 'earthquakes',
      id: quakeID,
    }, {
      hover: true
    });

  }
});
```
<!--copyeditor disable magnitude -->
保存你的修改并刷新你的浏览器页面。现在，当你的鼠标移至某一地震要素，会发生两件事：
- 地震的震级，位置和日期会在侧边栏显示。
- 代表要素的圆圈的样式会根据返回的 `mag` 属性而被更改。

{{
<AppropriateImage imageId="featureStateFinal" alt="Screenshot showing the basemap that demonstrates how the feature state expression changes the styling of features" />
}}

当你移动鼠标离开某一地震要素，尽管圆圈会依旧保有相同的大小和颜色，但是侧边栏会继续显示该要素的信息，直至你的鼠标移至另一个要素。你会在下一步中解决这一问题。

## 重置 feature state
创建该网页程序的最后一步是：当用户鼠标移动离开某一个地震要素时，更新其 feature state。你会使用 `map.on('mouseleave')` 函数来设置当用户鼠标移开时的侧边栏显示。

粘贴以下代码到你的 Javacript 代码中，于最后的 `</script>` 标签上方：

```js
map.on("mouseleave", "earthquakes-viz", function() {
  if (quakeID) {
    map.setFeatureState({
      source: 'earthquakes',
      id: quakeID
    }, {
      hover: false
    });
  }
  
  quakeID = null;
  // Remove the information from the previously hovered feature from the sidebar
  magDisplay.textContent = '';
  locDisplay.textContent = '';
  dateDisplay.textContent = '';
  // Reset the cursor style
  map.getCanvas().style.cursor = '';
});
```

保存你的修改，然后刷新在你浏览器中的页面。现在当你的鼠标移至某一地震要素再移开后，侧边栏会重置，直到你的鼠标移至另一个地震要素。

## 最终成品
<!--copyeditor ignore magnitude -->
你已经创建了一个使用 feature state 来根据地震震级，动态赋予地图上的地震要素样式的网页程序了。

{{
  <DemoIframe src="/help/demos/create-interactive-hover-effects-with-mapbox-gl-js/index.html" />
}}

最后的 HTML 文档会和以下一样：

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Create interactive hover effects with Mapbox GL JS</title>
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

    .quakeInfo {
      position: absolute;
      font-family: sans-serif;
      margin-top: 5px;
      margin-left: 5px;
      padding: 5px;
      width: 30%;
      border: 2px solid black;
      font-size: 14px;
      color: #222;
      background-color: #fff;
      border-radius: 3px;
    }
  </style>
</head>

<body>

  <div id='map'></div>
  <div class='quakeInfo'>
    <div><strong>Magnitude:</strong> <span id='mag'></span></div>
    <div><strong>Location:</strong> <span id='loc'></span></div>
    <div><strong>Date:</strong> <span id='date'></span></div>
  </div>

  <script>
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.44121, 37.76132], // Specify the starting position [lng, lat]
      zoom: 3.5 // Specify the starting zoom
    });

    // Target the relevant span tags in the quakeInfo div
    var magDisplay = document.getElementById('mag');
    var locDisplay = document.getElementById('loc');
    var dateDisplay = document.getElementById('date');

    // JavaScript date constructor:
    // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
    var today = new Date();
    // Use JavaScript to get the date a week ago
    var priorDate = new Date().setDate(today.getDate() - 7);
    // Set that to an ISO8601 timestamp as required by the USGS earthquake API
    var priorDateTs = new Date(priorDate);
    var sevenDaysAgo = priorDateTs.toISOString();

    map.on('load', function() {

      map.addSource('earthquakes', {
        'type': 'geojson',
        'data': 'https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&eventtype=earthquake&minmagnitude=1&starttime=' + sevenDaysAgo,
        'generateId': true // This ensures that all features have unique IDs
      });

      map.addLayer({
        'id': 'earthquakes-viz',
        'type': 'circle',
        'source': 'earthquakes',
        'paint': {
          // The feature-state dependent circle-radius expression will render
          // the radius size according to its magnitude when
          // a feature's hover state is set to true
          'circle-radius': [
            'case',
            ['boolean',
              ['feature-state', 'hover'],
              false
            ],
            [
              'interpolate', ['linear'],
              ['get', 'mag'],
              1, 8,
              1.5, 10,
              2, 12,
              2.5, 14,
              3, 16,
              3.5, 18,
              4.5, 20,
              6.5, 22,
              8.5, 24,
              10.5, 26
            ],
            5
          ],
          'circle-stroke-color': '#000',
          'circle-stroke-width': 1,
          // The feature-state dependent circle-color expression will render
          // the color according to its magnitude when
          // a feature's hover state is set to true
          'circle-color': [
            'case',
            ['boolean',
              ['feature-state', 'hover'],
              false
            ],
            [
              'interpolate', ['linear'],
              ['get', 'mag'],
              1, '#fff7ec',
              1.5, '#fee8c8',
              2, '#fdd49e',
              2.5, '#fdbb84',
              3, '#fc8d59',
              3.5, '#ef6548',
              4.5, '#d7301f',
              6.5, '#b30000',
              8.5, '#7f0000',
              10.5, '#000'
            ],
            '#000'
          ]
        }
      });

    });

    var quakeID = null;

    map.on('mousemove', 'earthquakes-viz', (e) => {

      map.getCanvas().style.cursor = 'pointer';
      // Set variables equal to the current feature's magnitude, location, and time
      var quakeMagnitude = e.features[0].properties.mag;
      var quakeLocation = e.features[0].properties.place;
      var quakeDate = new Date(e.features[0].properties.time);

      // Check whether features exist
      if (e.features.length > 0) {
        // Display the magnitude, location, and time in the sidebar
        magDisplay.textContent = quakeMagnitude;
        locDisplay.textContent = quakeLocation;
        dateDisplay.textContent = quakeDate;

        // If quakeID for the hovered feature is not null,
        // use removeFeatureState to reset to the default behavior
        if (quakeID) {
          map.removeFeatureState({
            source: "earthquakes",
            id: quakeID
          });
        }

        quakeID = e.features[0].id;
        
        // When the mouse moves over the earthquakes-viz layer, set the
        // feature state for the feature under the mouse
        map.setFeatureState({
          source: 'earthquakes',
          id: quakeID,
        }, {
          hover: true
        });

      }
    });

    map.on("mouseleave", "earthquakes-viz", function() {
      
      if (quakeID) {
        map.setFeatureState({
          source: 'earthquakes',
          id: quakeID
        }, {
          hover: false
        });
      }
      quakeID = null;
      // Remove the information from the previously hovered feature from the sidebar
      magDisplay.textContent = '';
      locDisplay.textContent = '';
      dateDisplay.textContent = '';
      // Reset the cursor style
      map.getCanvas().style.cursor = '';
    });
  </script>

</body>

</html>
```

## 下一步
如果想要了解更多关于 feature state expressions 和如何使用它们来动态赋予地图要素样式，你可以查看下列资源：
- 浏览 Mapbox GL JS 文档，了解 [`setFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate)， [`removeFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#removefeaturestate)， 和 [`getFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#getfeaturestate)。
- 查看 Mapbox 是如何使用 feature state 来创建一张使用2016年总统大选数据的地图。请见博客 [Live Electoral Maps: A Guide to Feature State](https://blog.mapbox.com/going-live-with-electoral-maps-a-guide-to-feature-state-b520e91a22d)。
- 了解更多关于使用 event 和 feature state 来针对各要素创建不同的样式变化。请见 [Create a hover effect example](https://docs.mapbox.com/mapbox-gl-js/example/hover-styles/)。
- 了解更多关于如何使用 Mapbox GL JS expressions。请见 [Get started with Mapbox GL JS expressions](/help/tutorials/mapbox-gl-js-expressions/) 教程。
