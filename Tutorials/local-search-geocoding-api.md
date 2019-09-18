---
title: 使用Geocoding API进行本地搜索
description: 本教程将指导您使用Mapbox Geocoding API中的可选参数创建本地搜索应用。
thumbnail: localSearchGeocodingApi
level: 2
language:
- JavaScript
prereq: 熟悉前端开发概念。
topics:
  - web apps
  - geocoding
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

Mapbox Geocoding API允许您进行正向地理编码，这意味着像`University of California Berkeley`这样的文本查询将转换为经纬度坐标。但有时仅仅找到查询结果是不够的。通常，您希望geocoder查找并偏向某个位置、限制在某个特定区域或两者兼而有之的查询结果。

Mapbox geocoder具有内置的排序功能，可以影响返回结果的顺序。（请阅读[How geocoding works](/help/how-mapbox-works/geocoding/#search-result-prioritization) 指南中有关搜索结果排序的更多信息）还可以通过包含可选的查询参数使 Geocoding API请求更具体。

在本教程中，您将使用Geocoding API的“proximity”和“bbox”参数为UC Berkeley创建一个本地搜索应用，该应用将结果限制在伯克利区域，并在校园内对搜索结果进行偏移。

<iframe width='100%' height='360px' frameBorder='0' src='/help/demos/local-search-geocoding-api/index.html'>&nbsp;</iframe>
<em class='small quiet'>查看<a href='/help/demos/local-search-geocoding-api/index.html'>完成的地图</a>。</em>

## 入门指南
要完成本教程，您需要：
- **一个Mapbox账户和access token。** 在 [mapbox.com/signup](https://www.mapbox.com/signup/)上注册一个账户。 您的 access tokens 位于您的[Account page](https://www.mapbox.com/account)。
- **Mapbox GL JS。** Mapbox GL JS是用于构建Web地图的JavaScript API。
- **一个文本编辑器。** 使用您选择的文本编辑器编写HTML，CSS和JavaScript。

## Geocoding API 查询结构
Mapbox的所有API访问都必须指定正在使用的API服务和API版本号：
```
https://api.mapbox.com/{api_service}/{version}
```

本教程中使用的API服务是`geocoding` ，版本号是`v5`。
```
https://api.mapbox.com/geocoding/v5
```

对Geocoding API的调用还必须包括正在使用的端点，该端点可以是`mapbox.places`或`mapbox.places-permanent`。(`mapbox.places-permanent`允许永久存储结果和批量地理编码，并且仅对拥有永久地理编码许可证的[企业客户](https://www.mapbox.com/enterprise)可用。)

下面示范使用`mapbox.places`端点。
```
https://api.mapbox.com/geocoding/v5/mapbox.places
```

### 必需参数
对Geocoding API的查询必须包含搜索文本(_search text_)。 搜索文本可以是正向地理编码的文本字符串，也可以是逆向地理编码的一组坐标。这个正向地理编码示例的搜索文本是 `San Francisco`：

```
https://api.mapbox.com/geocoding/v5/mapbox.places/San%20Francisco.json?access_token={{<UserAccessToken />}}
```

无论您是执行正向还是反向地理编码，搜索文本后面都需要跟`.json`，因为响应将返回GeoJSON对象。

### 可选参数
有趣的来了！Geocoding API的可选参数允许您自定义查询，以便您获取与您最相关的结果。 有关正向地理编码请求可以使用的可选参数的完整列表，请参阅[Geocoding API 文档](https://docs.mapbox.com/api/search/#forward-geocoding)。

本教程将使用两个可选参数，这两个参数有助于将结果偏向于特定的地理位置： `proximity` 和 `bbox`。


{{<Note title="查看API请求的结果" imageComponent={<BookImage />}>}}
  要查看之后部分示例中的查询结果，请复制API调用并将其粘贴到浏览器的地址栏中。在每个示例的末尾添加您自己的Mapbox访问令牌(access token)。您将看到API查询输出以GeoJSON格式的响应。
{{</Note>}}


#### proximity参数
`proximity`参数允许您将响应偏向于更接近指定位置的结果。这将确保更接近该位置的查询结果优先于更远处的查询结果。参数必须按照“经度纬度”顺序格式化为两个逗号分隔的坐标。要查找位置的坐标，可以使用[Mapbox Search Playground](https://www.mapbox.com/search-playground)。

```
# 优先考虑在San Francisco的位置
https://api.mapbox.com/geocoding/v5/mapbox.places/peets.json?proximity=-122.3995752,37.7881856&access_token={{<UserAccessToken />}}
```

```
# 优先考虑在Berkeley及其周围的位置
https://api.mapbox.com/geocoding/v5/mapbox.places/peets.json?proximity=-122.2727469,37.8715926&access_token={{<UserAccessToken />}}
```

由于`proximity`参数不存在排他性，因此它不会将结果限制为某个区域内，但会在更远的相关结果之前返回接近提供的坐标的相关结果。

#### bbox参数
`bbox`参数允许您将结果限制为仅包含在提供的边界框中的结果。 边界框需要格式化为以逗号分隔的四个坐标，以“minLon，minLat，maxLon，maxLat”顺序排列。

您可以使用任何坐标作为边界框，只要它们描述框形状即可。 要查找边界框的坐标，可以使用[Mapbox Search Playground](https://www.mapbox.com/search-playground).

```
# 在Washington DC寻找Starbucks
https://api.mapbox.com/geocoding/v5/mapbox.places/starbucks.json?bbox=-77.083056,38.908611,-76.997778,38.959167&access_token={{<UserAccessToken />}}
```

`bbox`参数具有排他性，这意味着它将排除超出指定边界的任何结果。

### 构建Geocoding API 查询
既然您已经了解了如何使用 Geocoding API的一些可选参数来将结果偏向某个位置并将结果限制在某个区域内，那么您可以在应用中使用它们了。本教程将引导您完成创建一个应用的过程，该应用将结果限制在一个设置区域内，然后将结果偏向一个地标。在这种情况下，设置的区域将是加利福尼亚州的伯克利(Berkeley California)，地标将是加州大学伯克利(UC Berkeley)分校。

使用cURL，Geocoding API查询，使用`proximity`来偏向Berkeley校园周围的结果，并使用`bbox`将结果限制为Berkeley区域，如下所示：
```
# 搜索文本是 "coffee"
# `proximity`设置为校园的坐标
# `bbox`设置为包含加利福尼亚州伯克利的坐标
https://api.mapbox.com/geocoding/v5/mapbox.places/coffee.json?proximity=-122.25948,37.87221&bbox=-122.30937,37.84214,-122.23715,37.89838&access_token={{<UserAccessToken />}}
```

## Geocoding 插件和库
Geocoding API的可选参数为您提供了自定义查询的强大方法，但在应用中使用原始cURL API调用可能很笨拙。Mapbox geocoder可通过几个插件和包装库获得并且还可以帮助您将其集成到应用中：
- [Mapbox GL JS Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder)
- [Mapbox.js Geocoder](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-mapbox-geocoder/)
- [Mapbox Java SDK](https://www.mapbox.com/android-docs/java-sdk/examples/)
- [MapboxGeocoder.swift](https://github.com/mapbox/MapboxGeocoder.swift)
- [Mapbox JavaScript SDK](https://github.com/mapbox/mapbox-sdk-js)
- [React Geocoder](https://github.com/mapbox/react-geocoder)

本教程使用Mapbox GL JS Geocoder插件。

## 创建您的应用
要创建本地搜索应用，您将创建一个HTML文件并初始化地图。 然后添加Mapbox GL JS Geocoder插件并设置`bbox`和`proximity`参数。

应用运行后，您将使用浏览器的开发者工具查看浏览器如何解析Geocoder插件的API请求。

### HTML文件
打开文本编辑器并创建一个名为`index.html`的新文件。 通过复制以下代码到文本编辑器中来设置此HTML文件。 此代码创建了页面的结构。

在页面的`<body>`中有一个ID属性为`map`的`<div>`元素。这个`<div>`是在页面上显示地图的容器。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset='utf-8' />
  <title>Local search app</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
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

</body>
</html>
```

### 初始化地图
接下来，您将添加Mapbox GL JS代码初始化地图，该地图将显示在您在上一步中创建的`<div>`中。将以下代码段置于结束标记`</body>`之上。确保设置了`mapbox.accessToken`等于您的Mapbox访问令牌(access token)。

```html
<script>
  mapboxgl.accessToken = '{{<UserAccessToken />}}';
  var map = new mapboxgl.Map({
    container: 'map', // Container ID
    style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Map style to use
    center: [-122.25948, 37.87221], // Starting position [lng, lat]
    zoom: 12, // Starting zoom level
  });
</script>
```

这段Mapbox GL JS代码为地图设置了样式，提供了中心点的坐标，并设置缩放等级。

保存您的更改。在浏览器中打开HTML文件查看渲染的地图。

![Screenshot showing a rendered Mapbox map](/help/img/geocoding/geocoding-initial-map.png)

### 在地图中添加标记(marker)
下一步是在校园地图上的坐标处添加一个标记，来显示地标的位置。

在完成上一步中编写的初始化代码后，添加以下代码段来向地图上添加标记:

```js
var marker = new mapboxgl.Marker() // initialize a new marker
  .setLngLat([-122.25948, 37.87221]) // Marker [lng, lat] coordinates
  .addTo(map); // Add the marker to the map
```

保存更改并在浏览器中刷新页面。在地图上指定的坐标处会有一个标记。

### 集成地理编码器(geocoder)
下一步是使用Mapbox GL JS Geocoder插件集成地理编码器(geocoder)。要做到这一点，首先需要将地理编码器(geocoder)的JavaScript和CSS的链接添加到HTML文件的头部。

```html
<script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
<link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />
```

添加这些链接后，您就可以在应用中使用Mapbox GL JS Geocoder插件。 接下来，在HTML文件中的结束标记`</ script>`上方添加以下代码。

```js
var geocoder = new MapboxGeocoder({ // Initialize the geocoder
  accessToken: mapboxgl.accessToken, // Set the access token
  mapboxgl: mapboxgl, // Set the mapbox-gl instance
  marker: false, // Do not use the default marker style
});

// Add the geocoder to the map
map.addControl(geocoder);
```

您正在为将搜索结果限制在特定位置的教程构建应用。为了让用户直观地看见这一点，您将使用Geocoder中的`placeholder`参数来设置要在搜索栏中显示的自定义文本。

在访问令牌(access token)之后，将下面这行代码添加到插件：
```
placeholder: 'Search for places in Berkeley'
```

保存更改。在浏览器中刷新页面，您将看到地图中添加了一个带有自定义文本的地理编码器(geocoder)搜索框。在搜索框中输入搜索词并选择结果时，地图会偏心到该位置。

![Screenshot showing the Mapbox GL JS Geocoder plugin added to a map](/help/img/geocoding/geocoding-geocoder-added.png)

### 添加bbox和proximity参数
在上一步添加的`map.addControl`语句中，在 `placeholder`参数后面添加“bbox”和“proximity”参数。

在Mapbox GL JS Geocoder插件中，`bbox`参数必须格式化为一个数组。`proximity`参数必须格式化为具有“longitude”属性和“latitude”属性的对象。（有关如何格式化查询参数的更多信息，请参阅[Mapbox GL JS Geocoder插件文档](https://github.com/mapbox/mapbox-gl-geocoder/blob/master/API.md)。）

添加这些参数后，整个语句将如下所示：

```js
var geocoder = new MapboxGeocoder({ // Initialize the geocoder
  accessToken: mapboxgl.accessToken, // Set the access token
  mapboxgl: mapboxgl, // Set the mapbox-gl instance
  marker: false, // Do not use the default marker style
  placeholder: 'Search for places in Berkeley', // Placeholder text for the search bar
  bbox: [-122.30937, 37.84214, -122.23715, 37.89838], // Boundary for Berkeley
  proximity: {
    longitude: -122.25948,
    latitude: 37.87221
  } // Coordinates of UC Berkeley
});
```

保存HTML文件并在浏览器中刷新页面。 现在，当您在地理编码器(geocoder)的搜索框中输入搜索时，您将不会收到在边界框之外的任何结果。 地理编码器返回的结果根据其与伯克利(Berkeley)校区的距离进行加权。

### 在选定的结果上放置标记

{{<Note title="添加自定义样式标记" imageComponent={<BookImage />}>}}
  Mapbox GL Geocoder在搜索结果位置会设置默认标记。此示例将在新图层上添加自定义标记。 如果要使用地理编码器提供的默认标记，请从新的地理编码器实例中删除`marker: false,`行。
{{</Note>}}

创建此应用的最后一步是在地图上选定搜索结果的位置放置自定义标记。 执行此操作的逻辑需要包含在[`map.on('load')` 事件](https://www.mapbox.com/mapbox-gl-js/api/#map#on)中，避免在加载地图之前触发它。 在结束标记`</ script>`之前，粘贴以下JavaScript：

```js
// After the map style has loaded on the page,
// add a source layer and default styling for a single point
map.on('load', function() {
  map.addSource('single-point', {
    type: 'geojson',
    data: {
      type: 'FeatureCollection',
      features: []
    }
  });

  map.addLayer({
    id: 'point',
    source: 'single-point',
    type: 'circle',
    paint: {
      'circle-radius': 10,
      'circle-color': '#448ee4'
    }
  });

  // Listen for the `result` event from the Geocoder
  // `result` event is triggered when a user makes a selection
  //  Add a marker at the result's coordinates
  geocoder.on('result', function(e) {
    map.getSource('single-point').setData(e.result.geometry);
  });
});
```

保存HTML文件并在浏览器中刷新页面。搜索并选择结果时，标记将放置在结果的坐标处。

### 在开发者工具中查看API
当你使用Mapbox GL JS Geocoder插件想要查看后台工作情况时，可以使用浏览器的开发者工具查看原始API调用。如果返回的结果不是所需的结果，则这对于调试查询非常有用。

{{<Note title="如何打开开发者工具？" imageComponent={<BookImage />}>}}

  以下说明是基于谷歌浏览器（chrome）的开发者工具布局。对于其他浏览器，细节上可能会有所不同，但一般来说，工作流程是相似的。关于如何打开开发者工具和查看网络详细信息，请阅读浏览器的帮助页。

{{</Note>}}

1. 在浏览器中加载您在本教程中创建的页面，如果该页面已打开，请刷新它。

1. 打开浏览器的开发工具。（在chrome中，您可以通过键入'command+option+i'或'command+option+j'来完成此操作。）

1. 在应用的地理编码器(geocoder)搜索栏中输入文本短语并选择结果。（比如下面例子中的“coffee”所搜词。）

1. 点击Network

1. 在“筛选”搜索栏中，输入"geocoding"。这将把网络调用列表缩小到Mapbox Geocoding API所做的调用。

1. 您可能会在调用列表中看到不止一个Geocoding API，每个调用代表搜索文本的不同阶段。单击包含完整搜索文本的选项（例如，“coffee”而不是“coff”）。

1. 在URL请求部分，您将看到一个类似于您在本教程[Build the Geocoding API query](#build-the-geocoding-api-query)中创建的cURL API请求的请求：

```
https://api.mapbox.com/geocoding/v5/mapbox.places/coffee.json?access_token={{<UserAccessToken />}}&proximity=-122.259%2C37.872&bbox=-122.30937%2C37.84214%2C-122.23715%2C37.89838&limit=5
```
浏览器返回的查询与之前创建的查询的区别在于，此次查询还包含了`limit`参数，并传入默认值 `5` 。

## 最终成品
你已经完成了一款本地搜索应用，当用户使用地理编码器(geocoder)搜索框中输入查询时，会将UC Berkeley校园周围的结果进行偏差，并排除位于Berkeley区域之外的任何结果。

<iframe width='100%' height='360px' frameBorder='0' src='/help/demos/local-search-geocoding-api/index.html'>&nbsp;</iframe>
<em class='small quiet'>View <a href='/help/demos/local-search-geocoding-api/index.html'>finished map</a>.</em>

最终的HTML文件如下：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8' />
    <title>Local search app</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
    <link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />
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
  mapboxgl.accessToken = '{{<UserAccessToken />}}';
  var map = new mapboxgl.Map({
    container: 'map', // Container ID
    style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Map style to use
    center: [-122.25948, 37.87221], // Starting position [lng, lat]
    zoom: 12, // Starting zoom level
  });

  var marker = new mapboxgl.Marker() // Initialize a new marker
    .setLngLat([-122.25948, 37.87221]) // Marker [lng, lat] coordinates
    .addTo(map); // Add the marker to the map

  var geocoder = new MapboxGeocoder({ // Initialize the geocoder
    accessToken: mapboxgl.accessToken, // Set the access token
    mapboxgl: mapboxgl, // Set the mapbox-gl instance
    marker: false, // Do not use the default marker style
    placeholder: 'Search for places in Berkeley', // Placeholder text for the search bar
    bbox: [-122.30937, 37.84214, -122.23715, 37.89838], // Boundary for Berkeley
    proximity: {
      longitude: -122.25948,
      latitude: 37.87221
    } // Coordinates of UC Berkeley
  });

  // Add the geocoder to the map
  map.addControl(geocoder);

  // After the map style has loaded on the page,
  // add a source layer and default styling for a single point
  map.on('load', function() {
    map.addSource('single-point', {
      type: 'geojson',
      data: {
        type: 'FeatureCollection',
        features: []
      }
    });

    map.addLayer({
      id: 'point',
      source: 'single-point',
      type: 'circle',
      paint: {
        'circle-radius': 10,
        'circle-color': '#448ee4'
      }
    });

    // Listen for the `result` event from the Geocoder
    // `result` event is triggered when a user makes a selection
    // Add a marker at the result's coordinates
    geocoder.on('result', function(ev) {
      map.getSource('single-point').setData(ev.result.geometry);
    });
  });
</script>
</body>
</html>
```

## 下一阶段
你可以做很多事情来构建这个应用，你可以 :
- 使用Turf.js分析来自加州大学伯克利分校(UC Berkeley)的各种的距离（请参阅[Sort stores by distance](/help/tutorials/geocode-and-sort-stores/)教程。）
- 尝试使用Mapbox GL JS插件中的`filter`功能来得到更多详细的结果（请参阅[Limit geocoder results to a named region](https://www.mapbox.com/mapbox-gl-js/example/mapbox-gl-geocoder-limit-region/)示例)。

