---
title: Build a store locator using Mapbox.js
description: Build a map application with Mapbox.js. This guide walks you through all the code that you need to build a store locator.
thumbnail: buildingAStoreLocatorJs
level: 3
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { sweetgreenLocations } from '../../snippets/sweetgreen-locations';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Build a store locator with Mapbox GL JS',
      link: '/help/tutorials/building-a-store-locator/'
    }}
  />
}}

在本教程中，您将学习如何在地图上创建商店位置标志。使用新地图，您将能够从侧边栏浏览位置列表，并选择特定商店以查看更多信息。在地图上选择特定商店 [marker](/help/glossary/marker/) ，侧边栏也将高亮显示。

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-four.html" />
}}

在本教程中，您将使用当地沙拉店[Sweetgreen](http://sweetgreen.com) 作为示例，他们有很多健康的地点，并且他们的沙拉很美味。
本指南通过[Mapbox.js](https://www.mapbox.com/mapbox.js/) 介绍了一些更高级的JavaScript概念。如果您是Mapbox.js的新手，我们建议您首先阅读我们的扩展与[Extending with Mapbox.js guide](/help/tutorials/extending-interactivity/) 指南。

## 现在开始

在动手写代码之前，请创建一个名为“store-locator”的本地文件夹来存放项目文件。此文件夹从此处开始称为*项目文件夹*
在我们开始之前，您需要熟悉一些内容：

- [**A tileset ID**](/help/glossary/tileset-id). tileset ID指向您使用Mapbox创建的唯一地图。出于本指南的目的，您将使用tileset ID `mapbox.k8xv42t9`，但如果您愿意，可以替换自己的自定义tileset！

- [**Your access token**](/help/glossary/access-token/).该访问令牌用于将地图与您的帐户相关联：

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
```

- [__Mapbox.js__](https://www.mapbox.com/mapbox.js/). 用于构建地图的Mapbox JavaScript API。

- __Data__. 为了您的方便，我们收集了Sweetgreen的位置并在GeoJSON中标记了数据。

- __Custom map marker__. 您的成品地图将会使用一些精美的自定义图像 [Save the image](/help/demos/store-locator/marker.png) 将图像保存到项目文件夹。

- __A text editor.__ 你将使用它编写HTML，CSS和JavaScript.

<h2 id='add-structure'>添加结构</h2>
在项目文件夹中，创建一个`index.html`文件。通过添加引用Mapbox.js JavaScript库及其附带的CSS来设置文档：

```html
<script src='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.js'></script>
<link href='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.css' rel='stylesheet' />
```
接下来，创建地图容器和侧边栏列表：

```html
<div class='sidebar pad2'>Listing</div>
<div id='map' class='map pad2'>Map</div>
```

应用一些CSS，然后可以看到布局的样子：

```css
body {
  background: #404040;
  color: #f8f8f8;
  font: 500 20px/26px 'Helvetica Neue', Helvetica, Arial, Sans-serif;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
}

/**
 * The page is split between map and sidebar - the sidebar gets 1/3, map
 * gets 2/3 of the page. You can adjust this to your personal liking.
 */
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
  <DemoIframe gl={false} src="/help/demos/store-locator/step-one.html" />
}}

## 初始化地图

现在您已经设置了项目的结构，通过使用Mapbox.js初始化您的地图。
首先，创建一个实例`L.mapbox.map`并将其存储在一个名为`map`的变量里。您还可以通过`setView`可以将地图视图放到商店所在的华盛顿特区。在这里，您需要更新您的tileset ID和访问令牌。在HTML下添加脚本：

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
var map = L.mapbox.map('map')
    .setView([38.909671288923, -77.034084142948], 13)
    .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
```
## 加载数据

在地图上放置任何标记之前，请将您上面下载的所有GeoJSON数据存储在一个名为`geojson`的变量中。初始化地图后，您可以通过`featureLayer.setGeoJSON`来引用`geojson`里的变量加载地图上的要素：

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
var geojson = {{sweetgreenLocations}};
var map = L.mapbox.map('map')
  .setView([38.909671288923, -77.034084142948], 13)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'))
  .featureLayer.setGeoJSON(geojson);
```

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-two.html" />
}}

或者，您可以将GeoJSON保存为`.geojson`文件并将文件加载到地图上。如果这样做，您将需要从本地Web服务器（类似http://localhost/store-locator.html） 运行您的应用程序。如果您尝试直接在浏览器中打开`index.html`，您将收到跨源资源共享（CORS）错误 [Cross-origin Resource Sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) 。

## 构建列表和工具条

地图上有一些标记，但您仍需要构建列表和工具提示。您不必要一个一个创建而可以将JavaScript用于读取GeoJSON并动态构建列表同时为我们设置工具提示。这意味着如果您需要添加位置，则只需更新GeoJSON即可。
`L.mapbox.featureLayer`允许您在使用该`eachLayer`方法将数据添加到地图之前迭代数据。这意味着JavaScript将遍历每个点，填充自定义工具提示，将每个位置列表添加到侧边栏，并在用户选中标记或者列表时监听并响应用户的点击事件。
```js
var locations = L.mapbox.featureLayer().addTo(map);
locations.setGeoJSON(geojson);
locations.eachLayer(function(locale) {
  // Iterate over each marker.
});
```
变量`locations`引用您的新变量`L.mapbox.featureLayer`，然后点击进入`eachLayer`。传递的参数`locale`是每个标记对象。
此时，您可以使用每个`locale`提供的信息去填充列表中的每一项。做的好！但您仍需要更新侧边栏HTML以保存列表信息：
```html
<div class='sidebar'>
  <div class='heading'>
    <h1>Our locations</h1>
  </div>
  <div id='listings' class='listings'></div>
</div>
```
接下来，更新您的CSS以适应您的布局更改：
```css
body {
  color: #404040;
  font: 400 15px/22px 'Helvetica Neue', Sans-serif;
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

.quiet {
  color: #888;
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

.listings .item:last-child {
  border-bottom: none;
}

.listings .item .title {
  display: block;
  color: #00853e;
  font-weight: 700;
}

.listings .item .title small {
  font-weight: 400;
}

.listings .item.active .title,
.listings .item .title:hover {
  color: #8cc63f;
}

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

.clearfix {
  display: block;
}

.clearfix::after {
  content: '.';
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}

/* Marker tweaks */
.leaflet-popup-close-button {
  display: none;
}

.leaflet-popup-content {
  font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
  padding: 0;
  width: 200px;
}

.leaflet-popup-content-wrapper {
  padding: 0;
}

.leaflet-popup-content h3 {
  background: #91c949;
  color: #fff;
  margin: 0;
  display: block;
  padding: 10px;
  border-radius: 3px 3px 0 0;
  font-weight: 700;
  margin-top: -15px;
}

.leaflet-popup-content div {
  padding: 10px;
}

.leaflet-container .leaflet-marker-icon {
  cursor: pointer;
}
```

现在，您可以对脚本进行最后润色。除了`eachLayer`，还要创建一个名为`listings`的变量，用于选择HTML中的列表容器。选中此选项后，您可以将每个列表附加到侧边栏中：

```js
var listings = document.getElementById('listings');

locations.eachLayer(function(locale) {
  // Shorten locale.feature.properties to `prop` so we're not
  // writing this long form over and over again.
  var prop = locale.feature.properties;

  var listing = listings.appendChild(document.createElement('div'));
  listing.className = 'item';

  var link = listing.appendChild(document.createElement('a'));
  link.href = '#';
  link.className = 'title';
  link.innerHTML = prop.address;

  if (prop.crossStreet) {
    link.innerHTML += ' <br /><small>' + prop.crossStreet + '</small>';
  }

  var details = listing.appendChild(document.createElement('div'));
  details.innerHTML = prop.city;

  if (prop.phone) {
    details.innerHTML += ' &middot; ' + prop.phoneFormatted;
  }
});
```

该`link`变量有一个特殊操作，可以平移地图上的标记。通过绑定`onclick`事件，您可以通过`locale`在上下文中定位当前对象，将地图平移到对象的坐标，并显示其工具条。

```js
link.onclick = function() {
  // 1. Toggle an active class for `listing`. View the source in the demo link for example.
  // 2. When a menu item is clicked, animate the map to center
  // its associated locale and open its popup.
  map.setView(locale.getLatLng(), 16);
  locale.openPopup();
};
```

每个标记工具提示都需要唯一的信息。使用`bindPopup`方法将内容传递到弹出窗口。

```js
var popup = 'Sweetgreen';
locale.bindPopup(popup);
```

最后，确保当用户单击标记时，通过给每一个`locale`绑定`click`事件，侧边栏中的关联列表状态设置为激活。

```js
locale.on('click', function() {
  // 1. Toggle an active class for `listing`. View the source in the demo link for example.

  // 2. center the map on the selected marker.
  map.setView(locale.getLatLng(), 16);
});
```
此时您所有的脚本应该像下面所示：

```js
var listings = document.getElementById('listings');
var locations = L.mapbox.featureLayer().addTo(map);

locations.setGeoJSON(geojson);

function setActive(el) {
  var siblings = listings.getElementsByTagName('div');
  for (var i = 0; i < siblings.length; i++) {
    siblings[i].className = siblings[i].className
      .replace(/active/, '').replace(/\s\s*$/, '');
  }

  el.className += ' active';
}

locations.eachLayer(function(locale) {

  // Shorten locale.feature.properties to `prop` so you don't
  // have to write this long form over and over again.
  var prop = locale.feature.properties;

  // Each marker on the map.
  var popup = '<h3>Sweetgreen</h3><div>' + prop.address;

  var listing = listings.appendChild(document.createElement('div'));
  listing.className = 'item';

  var link = listing.appendChild(document.createElement('a'));
  link.href = '#';
  link.className = 'title';

  link.innerHTML = prop.address;
  if (prop.crossStreet) {
    link.innerHTML += '<br /><small class="quiet">' + prop.crossStreet + '</small>';
    popup += '<br /><small class="quiet">' + prop.crossStreet + '</small>';
  }

  var details = listing.appendChild(document.createElement('div'));
  details.innerHTML = prop.city;
  if (prop.phone) {
    details.innerHTML += ' &middot; ' + prop.phoneFormatted;
  }

  link.onclick = function() {
    setActive(listing);

    // When a menu item is clicked, animate the map to center
    // its associated locale and open its popup.
    map.setView(locale.getLatLng(), 16);
    locale.openPopup();
    return false;
  };

  // Marker interaction
  locale.on('click', function(e) {
    // 1. center the map on the selected marker.
    map.panTo(locale.getLatLng());

    // 2. Set active the markers associated listing.
    setActive(listing);
  });

  popup += '</div>';
  locale.bindPopup(popup);
});
```

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-three.html" />
}}

`eachLayer`函数内部有很多代码，因为它确保每个事件都绑定到其各自的元素。

## 添加自定义标记

您可以通过向GeoJSON中的每个要素添加属性键来为我们的标记添加样式，但是对于此示例，您希望为您的商店提供唯一且精美的标记。
为了给商店添加标记，使用 之前创建的`locations.eachLayer`中的`setIcon`函数。通过在 [`L.icon`](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-icon/) 复制并粘贴以下内容后，传递您自己的自定义选项`locale.bindPopup(popup)`：

```js
locale.setIcon(L.icon({
  iconUrl: 'marker.png',
  iconSize: [56, 56],
  iconAnchor: [28, 28],
  popupAnchor: [0, -34]
}));
```

使用Source Sans Pro字体刷新地图的类型：

```html
<link href='https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700' rel='stylesheet'>
```
您还需要更新`body`的`font`属性：

```css
font:400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
```

## 完成作品

您完成了商店定位

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-four.html" />
}}

{{
<Button href="/help/demos/store-locator/store-locator-final.zip" passthroughProps={{ download: "store-locator-final" }} >
    <Icon name='arrow-down' inline={true} /> Download the completed project
</Button>
}}

如果您对从文件加载GeoJSON感兴趣，请参阅稍微修改过的代码。 [here's the slightly modified code](/help/demos/store-locator/store-locator-final-alt.zip).  当心！您需要提供这些文件以避免CORS错误。

## 下一步

不错的工作！我们希望您能够使用工具来创建自己的商店定位器。

如果将商店的位置数据添加到[Foursquare](https://foursquare.com) ，您可以通过直接从 [Foursquare's API](https://developer.foursquare.com/docs/)。 中提取数据来进一步扩展此示例。API请求返回地理定位信息和有关地点的详细信息。这将允许收到更多动态数据，例如用户提交的图像或位置已经接收的签到总数。
