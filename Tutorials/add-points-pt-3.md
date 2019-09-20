---
title: "Add points to a web map, part 3: add interactivity"
description: Add popups when markers are clicked using Mapbox GL JS.
thumbnail: addPointsToAMap
level: 1
topics:
- web apps
language:
- JavaScript
prependJs:
  - "import * as constants from '../../constants';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

这是 [tutorial series] (https://www.mapbox.com/studio-manual/help/#add-points-to-a-map) 的第三部分，也是最后一部分，它将教您如何使用 Mapbox Studio 数据集编辑器、Mapbox Studio 样式编辑器和 Mapbox GL JS.向地图添加点。

*第3部分* 重点介绍如何使用 **Mapbox GL JS** ，一个 JavaScript 库，并需要您编写代码。在本教程中，您将学习如何：
- 向 Mapbox GL JS 地图添加自定义样式
- 点击 [marker](/help/glossary/marker/) 时添加弹窗

{{
  <DemoIframe src="/help/demos/add-points-to-a-map/index.html" />
}}

## 准备开始

在本指南中，您需要遵循一些资源：

- **"芝加哥公园"的自定义样式**。你需要一个包含10个芝加哥公园标记点的 [style] (/help/glossary/style) 。您可以在 [Add points to a web map, part 1: create a dataset] (/help/tutorials/add-points-pt-1) 和 [Add points to a web map, part 2: create a style](/help/tutorials/add-points-pt-2) 中学习如何创建此样式。
- **开发环境**。本指南需要编写代码。有关如何开始的提示，请参照下面的 _准备编写代码_ 。

### 准备编写代码

使用弹窗创建交互式地图，您需要使用 [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api/) 。这需要编写代码。首先，您需要设置一个开发环境来编写HTML, CSS和JavaScript。如果您对编写代码还不熟悉，那么在使用 Mapbox GL J S之前，您可能需要研究 [Codecademy](https://www.codecademy.com/) 之类的资源，以了解有关前端开发如何工作的更多信息。你需要做的是：

- 下载文本编辑器（例如， [Sublime Text](https://www.sublimetext.com/) 或 [Atom](https://atom.io/)） 。
- 熟悉 JavaScript 和前端开发理念。

## 创建一个HTML 文件

在文本编辑器中创建新的 HTML 文件以初始化 Mapbox GL JS 地图。

### 初始化地图

1. 打开你的文本编辑器。
1. 将下面的代码复制并粘贴到文本编辑器中，以初始化您的 Mapbox GL JS 地图。
1. 确保将 `mapboxgl.accessToken` 设置和您的 access token 一致。
    - 当您登录到 [Mapbox Account] (https://www.mapbox.com/account) 时，您可以在 [Access tokens page](https://www.mapbox.com/account/access-tokens/) 上找到您的 access token。
1. 用您自己的样式URL替换 `your-style-URL-here` 。[Need help finding your style URL?] (/help/glossary/style-url/) 
1. 将您的文件另存为“index.html”。
1. 在浏览器中打开此文件。
1. 您应该可以在浏览器窗口中看到显示您的数据的地图。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Points on a map</title>
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
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}'; // replace this with your access token
    var map = new mapboxgl.Map({
      container: 'map',
      style: 'your-style-URL-here', // replace this with your style URL
      center: [-87.661557, 41.893748],
      zoom: 10.7
    });
    // code from the next step will go here
    </script>
  </body>
</html>
```

## 添加弹窗

在您成功显示地图后，需要再添加一点代码，以允许用户与标记点进行交互。这些代码包括：
  - [`queryrenderedfeatures`](https://www.mapbox.com/mapbox-gl-js/api/#map#queryrenderedfeatures) ：这个 Mapbox GL JS 方法将生成地图上所有点的列表以及与每个点相关联的特性属性。
  - [`mapboxgl.Popup`](https://www.mapbox.com/mapbox-gl-js/api/#popup) ：此方法用于创建显示某些功能属性的弹窗。`Popup` 组件有几个不同的实例成员，您可以使用它们自定义 popup 元素。在本例中，您将使用：
      - **`Popup.setLngLat()`:** 设置弹窗锚点的地理位置。
      - **`Popup.setHTML()`:** 将弹窗的内容设置为以字符串形式提供的 HTML。指定的属性必须与要在弹窗中显示的属性的名称匹配。在下面的代码中，将显示的属性是每个功能的 `title` 和 `description` 属性。
      - **`Popup.addTo(map)`:** 将弹窗添加到地图。
- 事件监听器：此事件监听器将确保仅当用户点击标记点时才显示弹窗。

### 添加更多代码

1. 将下面的代码复制并粘贴到您的HTML文件中，在初始化地图的代码之后，但在 `</script>` 标签之前。
1. 在变量 `features` 中，确保将 `layer-name-here` 替换为样式编辑器中显示的图层名称。如果您一直遵循本系列前面的教程，那么这里可能是 `chicago-parks` 。
1. 刷新浏览器页面。您可以点击标记点并在弹窗中看到标题和描述。

```js
map.on('click', function(e) {
  var features = map.queryRenderedFeatures(e.point, {
    layers: ['layer-name-here'] // replace this with the name of the layer
  });

  if (!features.length) {
    return;
  }

  var feature = features[0];

  var popup = new mapboxgl.Popup({ offset: [0, -15] })
    .setLngLat(feature.geometry.coordinates)
    .setHTML('<h3>' + feature.properties.title + '</h3><p>' + feature.properties.description + '</p>')
    .addTo(map);
});
```

## 最后成品

您已经使用 Mapbox Studio 数据集编辑器、Mapbox Studio 样式编辑器和 Mapbox GL JS 创建了一个地图，其中包含了自定义数据和样式，并允许用户交互。

{{
  <DemoIframe src="/help/demos/add-points-to-a-map/index.html" />
}}

## 下一步

要了解有关 Mapbox Studio 的更多操作，请浏览 [Mapbox Studio manual](https://www.mapbox.com/studio-manual/) 。有关 Mapbox GL JS 及其工作原理的更多信息，读我们的 [Mapbox web applications work](/help/how-mapbox-works/web-apps/) 指南。

