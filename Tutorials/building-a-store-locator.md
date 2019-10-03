---
title: Build a store locator using Mapbox GL JS
description: Build a map application with Mapbox GL JS. This guide walks you through all the code that you need to build a store locator.
thumbnail: buildingAStoreLocator
level: 3
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { sweetgreenLocations } from '../../snippets/sweetgreen-locations';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { DemoLink } from '../../components/demo-link';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---


此教程将展示如何利用Mapbix GL JS创建一个商店定位地图。您将可以通过侧边栏浏览所有的位置并选择一个位置以查看详细信息。从侧边栏中选择一个[标签](/help/glossary/marker/)可以进而标记地图上所选商店的位置。

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-five.html" />
}}

我们将以一个当地的沙拉店，[Sweetgreen](http://sweetgreen.com)，作为示例。他们拥有一系列的连锁店位置，而且他们的沙拉非常新鲜可口！

本教程将展示如何使用[Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/)创建一个交互式的网页地图。如果您是第一次使用Mapbox GL JS，我们建议您先阅读Mapbox所提供的关于[网络应用](/help/how-mapbox-works/web-apps/)的教程。

## 准备工作

首先，我们建议您创建一个本地文件夹，“store-locator”，以存放您的工程文件。在之后的教程中，我们称这个文件夹为*工程文件夹*。

您需要以下的资源：

- [__风格URL__](/help/glossary/style-url)：一个风格URL对应着您在Mapbox Studio中所创建一个地图风格。您可以在[Mapbox Studio风格编辑器](https://www.mapbox.com/studio-manual/reference/styles/)中创建一个自定义风格，或者使用[预设的风格](https://www.mapbox.com/studio/styles)。
- 账号[__秘钥__](/help/glossary/access-token/)：您需要一个秘钥来将您的账号和您的地图关联起来。您的秘钥可以在[账号信息页](https://www.mapbox.com/account/)获取。
- [__Mapbox GL JS__](https://www.mapbox.com/mapbox-gl-js/)：Mapbox JavaScript开发者库使用了WebGL来呈递Mapbox GL风格的交互式地图。
- __文本编辑器__：您需要能够编写THML、CSS以及JavaScript。
- __数据__：我们准备了一些Sweetgreen连锁店的位置信息，并编译成了GeoJSON格式的文件。
- __自定义地图标签__：您需要一张图片来作为您的地图标签。请自行选择并保存一张图片至您的工作文件夹中。

{{
<Button href="/help/demos/store-locator/marker.png" passthroughProps={{ download: "marker" }} >
    <Icon name='arrow-down' inline={true} />下载自定义的标签
</Button>
}}

## 页面布局设置

在您的工程文件夹中，创建一个文件并命名为`index.html`。在`head`中添加以下Mapbox GL JS和CSS代码：

```html
<script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

然后，我们需要标记此页面并创建一个地图容器和一个侧边栏：

```html
<div class='sidebar pad2'>Listing</div>
<div id='map' class='map pad2'>Map</div>
```

接下来，我们设置一些CSS以定义页面的布局：

```css
body {
  background: #404040;
  color: #f8f8f8;
  font: 500 20px/26px 'Helvetica Neue', Helvetica, Arial, Sans-serif;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
}

/*这个页面被分为了地图和侧边栏。侧边栏相对宽度为页面的三分之一，地图容器为三分之二。您可以自行调整相对宽度。*/
.sidebar {
  width: 33.3333%;
}

.map {
  border-left: 1px solid #fff;
  position: absolute;
  left: 33.3333%;
  width: 66.6666%;
  top: 0;
  bottom: 0;
}

.pad2 {
  padding: 20px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-one.html" />
}}

## 初始化地图

您已经完成了页面的布局设计，我们可以通过Mapbox GL JS来初始化我们的地图。

首先，在`mapboxgl.accessToken`中添加您的秘钥。然后，通过`new mapboxgl.Map()`创建一个新的`map`对象，并将其保存在变量`map`中：

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
// 在页面中添加一个地图
var map = new mapboxgl.Map({
  // HTML中所包含的容器ID
  container: 'map',
  // 风格URL
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  // 初始化的位置用[x, y]格式标记
  center: [-77.034084, 38.909671],
  // 初始的缩放程度
  zoom: 14
});
```

如您所见，Mapbox GL JS初始化地图的时候需要以下的设置：

- `contianer`：`<div>`的`id`元素标注了地图的显示位置。在上面的例子中，我们 的`id`是`map`。
- `style`：地图所选用的[风格URL](/help/glossary/style-url/)。在我们的例子中，{{ <DemoLink href="https://api.mapbox.com/styles/v1/mapbox/light-v{constants.VERSION_LIGHT_STYLE}.html?title=true&access_token=MapboxAccessToken#1.07/0.0/0.0" text="Mapbox Light map" /> }}包含了风格URL`mapbox://styles/mapbox/light-{{constants.VERSION_LIGHT_STYLE}}`。
- `center`：由[x, y]所标注的初始化地图中心位置。
- `zoom`：初始的地图缩放程度。

## 加载数据

在Mapbox GL JS中，地图的呈递过程在浏览器中实现。想要实现这一过程，您需要添加一个具有地理信息的图层以及对应的操作步骤。

您的代码需要能够访问地理信息才能够添加一个源地图。将所有的`sweetgreen.geojson`GeoJSON数据保存在变量`stores`中：

```js
var stores = {{ sweetgreenLocations }};
```

现在您可以添加一个图层并进一步定义这个图层应该如何显示。当地图通过`addLayer()`显示的时候，向地图中添加您的数据。创建一个新的图层，并设置`stores`为您的GeoJSON数据源。然后，添加如何显示数据的操作步骤。此教程仅使用了极简风格，如果您想要了解完整的图层风格设置信息，请阅读[Mapbox风格设置文档](https://www.mapbox.com/mapbox-gl-style-spec/)：

```js
map.on('load', function(e) {
  // 向地图中添加数据图层
  map.addLayer({
    id: 'locations',
    type: 'symbol',
    // 添加包含有坐标和附加信息的GeoJSON数据源
    source: {
      type: 'geojson',
      data: stores
    },
    layout: {
      'icon-image': 'restaurant-15',
      'icon-allow-overlap': true,
    }
  });
});
```

_请注意，`restaurant-15`指的是Mapbox轻风格中的一个图标。您在之前的步骤中已经添加了这个风格。_

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-two.html" />
}}

## 创建商店列表

您已经将商店的位置显示在了地图上，现在可以利用一个循环语句来自动创建包含所有商店位置信息的列表了。我们使用一个循环语句遍历所有的GeoJSON数据，这样一来，如果您需要修改或者添加商店位置信息，您**只需要**修改GeoJSON文件，而不需要改动任何的代码。

首先，我们需要改动HTML以保证列表信息的显示，同时相应的我们需要更改CSS格式设置：

```html
<div class='sidebar'>
  <div class='heading'>
    <h1>Our locations</h1>
  </div>
  <div id='listings' class='listings'></div>
</div>
```

```css
body {
  color: #404040;
  font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
}

* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

h1 {
  font-size: 22px;
  margin: 0;
  font-weight: 400;
  line-height: 20px;
  padding: 20px 2px;
}

a {
  color: #404040;
  text-decoration: none;
}

a:hover {
  color: #101010;
}

.sidebar {
  position: absolute;
  width: 33.3333%;
  height: 100%;
  top: 0;
  left: 0;
  overflow: hidden;
  border-right: 1px solid rgba(0, 0, 0, 0.25);
}

.pad2 {
  padding: 20px;
}

.map {
  position: absolute;
  left: 33.3333%;
  width: 66.6666%;
  top: 0;
  bottom: 0;
}

.heading {
  background: #fff;
  border-bottom: 1px solid #eee;
  height: 60px;
  line-height: 60px;
  padding: 0 10px;
}

.listings {
  height: 100%;
  overflow: auto;
  padding-bottom: 60px;
}

.listings .item {
  display: block;
  border-bottom: 1px solid #eee;
  padding: 10px;
  text-decoration: none;
}

.listings .item:last-child { border-bottom: none; }

.listings .item .title {
  display: block;
  color: #00853e;
  font-weight: 700;
}

.listings .item .title small { font-weight: 400; }

.listings .item.active .title,
.listings .item .title:hover { color: #8cc63f; }

.listings .item.active {
  background-color: #f8f8f8;
}

::-webkit-scrollbar {
  width: 3px;
  height: 3px;
  border-left: 0;
  background: rgba(0, 0, 0, 0.1);
}

::-webkit-scrollbar-track {
  background: none;
}

::-webkit-scrollbar-thumb {
  background: #00853e;
  border-radius: 0;
}

.clearfix { display: block; }

.clearfix::after {
  content: '.';
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
```

然后，我们定义一个方程。这个方程自动遍历所有的Sweetgreen位置，并且添加它们到侧边栏中：

```js
function buildLocationList(data) {
  // 遍历所有的商店
  for (i = 0; i < data.features.length; i++) {
    var currentFeature = data.features[i];
    // 重新命名data.feature.properties为`prop`
    // 以避免过长字符串的反复出现
    var prop = currentFeature.properties;
    // 选择列表容器的HTML元素
    // 为每一个商店添加一个item类的div
    var listings = document.getElementById('listings');
    var listing = listings.appendChild(document.createElement('div'));
    listing.className = 'item';
    listing.id = 'listing-' + i;

    // 为每一个商店添加一个title类的链接
    // 并将其与位置相互关联
    var link = listing.appendChild(document.createElement('a'));
    link.href = '#';
    link.className = 'title';
    link.dataPosition = i;
    link.innerHTML = prop.address;

    // 为每一个商店创建一个details类的div
    // 并添加相应的城市和电话号码
    var details = listing.appendChild(document.createElement('div'));
    details.innerHTML = prop.city;
    if (prop.phone) {
      details.innerHTML += ' &middot; ' + prop.phoneFormatted;
    }
  }
}
```

接下来，您可以通过调用这个方程来加载地图。您可以在`addLayer()`之后的`map.on('load', ...)`方程中调用这个方程`buildLocationList(stores);`。调用结果如下：

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-three.html" />
}}

## 创建可交互式地图

当用户点击地图上的某个点或者侧边栏中的一个链接的时候，我们希望以下事件的发生：

1. 地图自动显示商店的位置。
2. 在标签上方自动弹出一个窗口。
3. 选中的商店在侧边栏中高亮显示。

这看上去比较复杂，但是我们可以做到！

### 定义一个可交互式的方程

首先，我们需要两个方程：第一个方程能够将地图设置在正确的位置，第二个方程显示一个弹出窗口。这些方程会在用户点击侧边栏中的商店或者点击一个商店位置的时候同时被调用。我们将在之后创建我们的第三个方程来完成侧边栏的高亮显示功能。

```js
function flyToStore(currentFeature) {
  map.flyTo({
    center: currentFeature.geometry.coordinates,
    zoom: 15
  });
}

function createPopUp(currentFeature) {
  var popUps = document.getElementsByClassName('mapboxgl-popup');
  // 我们需要检查并移除已经存在的弹出窗口
  if (popUps[0]) popUps[0].remove();

  var popup = new mapboxgl.Popup({ closeOnClick: false })
    .setLngLat(currentFeature.geometry.coordinates)
    .setHTML('<h3>Sweetgreen</h3>' +
      '<h4>' + currentFeature.properties.address + '</h4>')
    .addTo(map);
}
```

您可以自定义您的弹出窗口的风格样式：

```css
/* Marker tweaks */
.mapboxgl-popup-close-button {
  display: none;
}

.mapboxgl-popup-content {
  font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
  padding: 0;
  width: 180px;
}

.mapboxgl-popup-content-wrapper {
  padding: 1%;
}

.mapboxgl-popup-content h3 {
  background: #91c949;
  color: #fff;
  margin: 0;
  display: block;
  padding: 10px;
  border-radius: 3px 3px 0 0;
  font-weight: 700;
  margin-top: -15px;
}

.mapboxgl-popup-content h4 {
  margin: 0;
  display: block;
  padding: 10px;
  font-weight: 400;
}

.mapboxgl-popup-content div {
  padding: 10px;
}

.mapboxgl-container .leaflet-marker-icon {
  cursor: pointer;
}

.mapboxgl-popup-anchor-top > .mapboxgl-popup-content {
  margin-top: 15px;
}

.mapboxgl-popup-anchor-top > .mapboxgl-popup-tip {
  border-bottom-color: #91c949;
}
```

为了`.remove()`能够后相兼容老版本的浏览器，您需要在脚本开头处添加下面的代码：

```js
// This will let you use the .remove() function later on
if (!('remove' in Element.prototype)) {
  Element.prototype.remove = function() {
    if (this.parentNode) {
      this.parentNode.removeChild(this);
    }
  };
}
```

请移步[HTML文档](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove)以获得详细信息。

### 添加时间响应机制

现在我们已经定义了两个方程，但是我们希望在用户点击的时候调用这两个方程。因此，我们需要添加_时间响应机制_，一旦用户做出了点击的操作，这个响应机制会自动检测到这个操作并调用一些方程。我们需要添加两个机制：一个机制响应对于侧边栏的点击，一个机制响应对于地图位置的点击。

下面的代码实现了对链接点击事件的响应：

```js
// 对链接点击的响应
link.addEventListener('click', function(e) {
  // 更新currentFeature至被点击的链接
  var clickedListing = data.features[this.dataPosition];
  // 1. 地图重定位
  flyToStore(clickedListing);
  // 2. 关闭其他所有的弹出窗口并显示新的弹出窗口
  createPopUp(clickedListing);
  // 3. 移除所有的高亮显示并高亮显示新的链接
  var activeItem = document.getElementsByClassName('active');
  if (activeItem[0]) {
    activeItem[0].classList.remove('active');
  }
  this.parentNode.classList.add('active');
});
```

下面的代码实现了对地图位置点击事件的响应：

```js
// 对地图位置点击事件的响应
map.on('click', function(e) {
  // 查询在视窗中所有的位置
  var features = map.queryRenderedFeatures(e.point, { layers: ['locations'] });
  if (features.length) {
    var clickedPoint = features[0];
    // 1. 地图重定位
    flyToStore(clickedPoint);
    // 2. 关闭其他所有的弹出窗口并显示新的弹出窗口
    createPopUp(clickedPoint);
    // 3. 移除所有的高亮显示并高亮显示新的链接
    var activeItem = document.getElementsByClassName('active');
    if (activeItem[0]) {
      activeItem[0].classList.remove('active');
    }
    // 查找store.features与接受点击事件的clickedPoint所关联的索引号
    var selectedFeature = clickedPoint.properties.address;

    for (var i = 0; i < stores.features.length; i++) {
      if (stores.features[i].properties.address === selectedFeature) {
        selectedFeatureIndex = i;
      }
    }
    // 选择被选中的商店并添加到active类中
    var listing = document.getElementById('listing-' + selectedFeatureIndex);
    listing.classList.add('active');
  }
});
```

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-four.html" />
}}

## 添加自定义标签

此部分的教程将展示如何使用自定义的地图标签。首先，您需要移除已存在的图层以及关联的方程。删除`.addLayer()`方程以移除图层，并添加`.addSource()`方程。之前我们使用`addLayer`方程来定义地图标签，但是现在我们要使用标签API来向GeoJSON数据中添加我们的标签图片：

```js
map.addSource('places', {
  type: 'geojson',
  data: stores
});
```

您也需要删除[响应标签点击事件的方程](#symbol-click)。我们之前创建了这个方程来完成地图重定位、显示弹出窗口以及高亮商店信息。然后，我们需要通过`mapboxgl.Marker()`添加我们自定义的Sweetgreen图标。与图表图层不同的是，图表图层包含自己的图标，但是`mapboxgl.Marker()`仅仅是HTML DOM元素，它可以进一步通过CSS来定义样式。添加一个`.marker`CSS样式然后将`background-image`设置为您之前已经[下载](/help/demos/store-locator/marker.png)好的Sweetgreen标签。

```css
.marker {
  border: none;
  cursor: pointer;
  height: 56px;
  width: 56px;
  background-image: url(marker.png);
  background-color: rgba(0, 0, 0, 0);
}
```

我们可以通过遍历所有的商店，向地图给每一个商店添加新的标签：

```js
stores.features.forEach(function(marker) {
  // 给标签创建一个div
  var el = document.createElement('div');
  // Add a class called 'marker' to each div
  el.className = 'marker';
  // 图片默认为中心显示。您可以调整显示的中心。
  // 创建自定义标签，调整中心位置，然后添加到地图中
  new mapboxgl.Marker(el, { offset: [0, -23] })
    .setLngLat(marker.geometry.coordinates)
    .addTo(map);
});
```

### 添加消息响应

现在您已经添加了自定义的标签，您需要重新定义点击事件的响应方程来实现地图重定位、弹出窗口的显示以及商店信息的高亮显示。在您的`forEach`方程中我们需要添加一个响应方程:

```js
el.addEventListener('click', function(e) {
  var activeItem = document.getElementsByClassName('active');
  // 1. 地图重定位
  flyToStore(marker);
  // 2. 关闭其他所有的弹出窗口并显示新的弹出窗口
  createPopUp(marker);
  // 3. 移除所有的高亮显示并高亮显示新的链接
  e.stopPropagation();
  if (activeItem[0]) {
    activeItem[0].classList.remove('active');
  }
  var listing = document.getElementById('listing-' + i);
  console.log(listing);
  listing.classList.add('active');
});
```

### 微调

再添加了标签之后，您需要调整自动弹出窗口的位置以防止遮挡。您需要修改一下CSS代码：

```css
.mapboxgl-popup {
  padding-bottom: 50px;
}
```

您也可以使用Source Sans Pro来更改您的风格：

```html
<link href='https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700' rel='stylesheet'>
```

您需要相应地修改`body`风格中`font`属性:

```css
font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
```

## 成果

您已经成功创建了一个商店定位地图。

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-five.html" />
}}

## 下一步

您已经具备了创建属于你自己的商店定位地图的能力。请前文[帮助页面](/help/tutorials/)以获取更多的Mapbox GL JS操作技巧。