刘年华 已完成 custom-markers-gl-js.md 翻译
@coffee-gh

---
title: Add custom markers in Mapbox GL JS
description: Add custom HTML markers, style them, and add tooltips with Mapbox GL JS.
thumbnail: customMarkersGlJs
level: 2
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---
在本教程中，您将学习如何使用 Mapbox GL JS 构建带有自定义标记 [markers](/help/glossary/marker/) 的交互式 Web 地图。Mapbox GL JS 是一个需要编写代码的JavaScript库。您将学会如何加载内联 [GeoJSON](/help/glossary/geojson) 数据并使用 HTML 标记自动添加到地图中。最后，您将学习如何在单击标记时添加弹出窗口。最终地图将如下所示：

{{
  <DemoIframe src="/help/demos/custom-markers-gl-js/index.html" />
}}

## 入门

对于此项目，我们建议您创建一个名为 `mapbox-markers` 的本地文件夹来保存项目文件。此文件夹将作为您的项目文件夹。

按照本指南进行操作，您需要提前准备以下文件：

- [__访问 token__](/help/glossary/access-token/)。在您的账号管理中，将访问 token 与地图相关联。您的访问 token 位于 [Account page](https://www.mapbox.com/account)。
- **文本编辑器** 您需要编写 HTML, CSS, and JavaScript
- **自定义图像**本教程使用自定义 HTML 标记的图像来显示办公室的位置。您需要下载 PNG 图像文件以用作自定义图标，并将其保存在与 index.html 文件相同的项目文件夹中。

{{
<Button href="/help/demos/custom-markers-gl-js/mapbox-icon.png" passthroughProps={{ download: "mapbox-icon" }} >
    <Icon name='arrow-down' inline={true} /> Download image
</Button>
}}

## 创建 Mapbox GL JS 地图

现在您已准备好使用Mapbox GL JS！首先，创建一个新的 HTML 文件并编写代码以初始化 Mapbox GL JS 地图。

### 初始化地图

1. 打开文本编辑器
2. 创建一个新的 HTML 文件
3. 将下面的代码复制并粘贴到文本编辑器中以初始化 Mapbox GL JS 地图
4. 确保您使用的是 API 访问 token 是 `mapboxgl.accessToken`
5. 命名为 `index.html` 并保存于项目文件夹中
6. 使用浏览器打开文件
7. 您应该会在浏览器窗口中看到一个初始化的 Mapbox GL JS 地图，其中显示了 Mapbox Light 样式。但是这个时候还没有地图标记。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8' />
    <title></title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
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
  container: 'map',
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  center: [-96, 37.8],
  zoom: 3
});

// code from the next step will go here!

</script>

</body>
</html>
```

正如所看到的，Mapbox GL JS 地图需要几个参数设置：

- `container`: 地图应存在于 `id` 集合中的 `<div>` 元素。在本教程中， `id` 集合中的 `<div>` 元素应该是 `'map'`。
- `style`: 地图演示。在本教程中，使用 Mapbox Light map 样式的地图应有以下的URL `mapbox://styles/mapbox/light-{{constants.VERSION_LIGHT_STYLE}}`。
- `center`: 地图初始中心点应以 `[longitude, latitude]` 格式设置
- `zoom`: 地图的初始缩放级别。

### 加载 GeoJSON 数据

将内联 GeoJSON 数据添加到 HTML 文件中，这样就能够加载数据。此 GeoJSON 将用于确定地图上的标记位置。

复制以下内容，粘贴在 `</script>` 标记之前，这样就能完成地图初始化操作。此代码声明一个变量 `geojson` ，值等于 GeoJSON 数据。

```js
var geojson = {
  type: 'FeatureCollection',
  features: [{
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.032, 38.913]
    },
    properties: {
      title: 'Mapbox',
      description: 'Washington, D.C.'
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.414, 37.776]
    },
    properties: {
      title: 'Mapbox',
      description: 'San Francisco, California'
    }
  }]
};
```

{{
  <Note imageComponent={<BookImage />}>
    <p>如果您有一个很大的 GeoJSON 文件，您可能希望将其作为外部文件加载而不是内联添加。您可以通过链接到其 URL（如果是远程托管），或使用 AJAX 调用在本地或从第三方 API 加载来实现。</p>
  </Note>
}}

## 添加 HTML 标记

现在您已经加载了数据，添加代码并为每个标记创建 HTML DOM 元素。使用 Mapbox GL JS [Marker](https://www.mapbox.com/mapbox-gl-js/api/#marker) 将其绑定到 GeoJSON 中。您将使用在本教程开头下载的图像，该图像应保存在项目文件夹中。

使用 Marker 方法添加标记时，会将空白 div 附加到 GeoJSON 的每个点。将标记添加到地图前，您需要指定标记的样式。

### 样式标记
background-image为名为的类marker。在同一个index.html文件中，将代码复制并粘贴style到#map声明下方的代码中。
首先，添加您需要设置标记样式的 CSS 。这个案例中，请将下载的图像文件作为背景图片 `background-image` 在一个 `marker`的集合中。在同一个文件件`index.html`中，复制下方的代码并粘贴至 `style` 标签下的 `#map` 声明中。

```css
.marker {
  background-image: url('mapbox-icon.png');
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}
```

### 将标记添加至地图中

接下来，将创建标记所需的 JavaScript 代码添加到地图中。在结束脚本标记之前，对象 `map` 声明结束，将以下代码复制并粘贴到`script` 标记中。

```js
// add markers to map
geojson.features.forEach(function(marker) {

  // create a HTML element for each feature
  var el = document.createElement('div');
  el.className = 'marker';

  // make a marker for each feature and add to the map
  new mapboxgl.Marker(el)
    .setLngLat(marker.geometry.coordinates)
    .addTo(map);
});
```

保存文件并刷新浏览器。您应该看到使用自定义 HTML 标记的地图。


## 添加弹窗

最后一步，使用 Mapbox GL JS 为您的标记添加弹窗，在 `mapboxgl.Marker` 声明中这样操作。

### 弹窗样式

首先，添加需要的 CSS 代码来设置弹窗样式。在同一 index.html 文件中，复制代码并粘贴到 `.marker` 声明下方的 `style` 标记中。

```css
.mapboxgl-popup {
  max-width: 200px;
}

.mapboxgl-popup-content {
  text-align: center;
  font-family: 'Open Sans', sans-serif;
}
```

### 将弹窗附在标记上

接下来，将包含每个点信息的弹窗所需的 JavaScript 添加至代码中，这样在单击标记时就能显示弹窗：

1. 复制下方的 `.setPopup` 代码，将其粘贴至  `script` 标签中，其位于 `.setLngLat()` 后和 `.addTo()` 前。
  -确保您使用正确的密钥来显示要在弹窗中展示的数据。在此示例中，您将显示数据 `title` 和 `description` 属性。
2. 保存文件并刷新浏览器。
3. 够单击标记并查看显示的弹窗。


```js
new mapboxgl.Marker(el)
  .setLngLat(marker.geometry.coordinates)
  .setPopup(new mapboxgl.Popup({ offset: 25 }) // add popups
    .setHTML('<h3>' + marker.properties.title + '</h3><p>' + marker.properties.description + '</p>'))
  .addTo(map);
```

请注意，在使用该 [`mapboxgl.Popup`](https://www.mapbox.com/mapbox-gl-js/api/#popup) 方法声明弹出窗口时，您已添加了偏移值，以确保弹窗位于标记的中心。


## 最终产品

您已使用 Mapbox GL JS 制作了包含自定义数据和样式的交互式标记贴图。
{{
  <DemoIframe src="/help/demos/custom-markers-gl-js/index.html" />
}}

## 下一步

现在您已经使用 Mapbox GL JS 创建了一个项目，我们建议您查浏览我们的其他教程以扩展您的 Web 应用程序：

- [Add points to a map](/help/tutorials/add-points-pt-1/) using Mapbox Studio and Mapbox GL JS.
- [Build a store locator](/help/tutorials/building-a-store-locator/) using Mapbox GL JS.
- [Show changes over time](/help/tutorials/show-changes-over-time/) with Mapbox GL JS.
- [Analyze data with Turf.js](/help/tutorials/analysis-with-turf/) and Mapbox GL JS.

浏览 [Mapbox GL JS examples](https://www.mapbox.com/mapbox-gl-js/examples/) 以探索更多内容，了解有关如何扩展项目和代码的更多想法，以帮助您更好地入门。
