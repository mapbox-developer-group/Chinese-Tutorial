---
title: 开始使用等时圈API
description: 使用Mapbox的等时圈API创建一个可以运行用户可视化在给定时间内，他们可以步行、骑车或者开车走多远距离的web app
thumbnail: 等时圈最终产品
topics:
- web apps
- navigation
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
contentType: tutorial
---

本教程展示了如何使用Mapbox等时线接口。此接口使用Mapbox的交通港式配置与行程时间，创建一个运行用户估计自己可以在一定的时间内，步行、骑车或开车走多远的Web应用。

{{
  <DemoIframe src="/help/demos/get-started-isochrone-api/index.html" />
}}

## 开始
为完成此教程，你需要:

- **Mapbox的接口许可.** 你的接口许可在你的 [用户界面](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) 是一个可以创建在线地图的 JavaScript API.
- **Mapbox 等时线 API.** The [等时线 API](https://docs.mapbox.com/api/navigation/#isochrone) 计算在指定的时间内，可以从一个地点到达的区域，返回可到达区域，并将结果的面或者线展示为可以在地图上绘制的等值线。  
- **Mapbox Assembly.** [Assembly](https://labs.mapbox.com/assembly/) 是一个可以用来设计你的应用的用户界面的开源的CSS框架。
- **jQuery.** [jQuery](https://jquery.com/) 是一个用来添加APP请求到应用中的 JavaScript 库.
- **文本编辑器.** 用你选择的文本编辑器来编辑HTML, CSS 和 JavaScript代码.

## 使用等时线 API
一个等时线API请求需要三个参数：

- **`profile`:**  查询接口所需要到的Mapbox的交通方式配置.  `walking` 代表步行或者远足的移动时间, `cycling` 代表骑车, 或者 `driving` 代表驾车方式计算移动时间.
- **`coordinates`:** 一对 `{经度,纬度}` 坐标，表示等时线的中心位置。
- **`contours_minutes`:** Times 用来描述一分钟内移动的耗时。可以用一个逗号分隔的四段时间组成的列表来描述，最大耗时为60分钟。

```
https://api.mapbox.com/isochrone/v1/mapbox/{profile}/{coordinates}.json?{contours_minutes}&access_token=YOUR_MAPBOX_ACCESS_TOKEN
```

等时线API还可以接受一些可选择的参数来自定义查询。这个APP中你将学习使用一个可选参数。

- `polygons`: 此参数明确了是否返回等时线为一个GeoJson格式的面或者线。当 `polygons=true` 时等时线闭合为一个环，并且返回为面格式。

想获得更多关于等时线API和他的其他可选参数，请参考[Isochrone API documentation](https://docs.mapbox.com/api/navigation/#isochrone).

此等时线查询样例使用 `driving` 交通方式配置,  `contours_minutes` 设置为15, 并将 `polygons` 参数设置为 `true`:

```
https://api.mapbox.com/isochrone/v1/mapbox/driving/-117.17282,32.71204?contours_minutes=15&polygons=true&access_token={{ <UserAccessToken /> }}
```

若想查看接口响应的Json，你可以将其粘贴在你的浏览器中。响应中的 `geometry` 对象包含了一组描述等时线外轮廓的坐标。同时响应还包含一个 `feature` 对象，描述等时线应该被如何绘制的参数，包括填充颜色，填充透明度。你将使用这些等时线API所返回的信息绘制并设计这些等时线，并将其添加到app的地图中。


## 创建地图
开始此APP，你首先需要使用 [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) 创建地图：

1. 打开你的文本编辑器.
1. 创建一个文件并命名为 `index.html`.
1. 粘贴如下代码到文本编辑器中，来启动新的HTML

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Isochrone API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- Import Assembly -->
  <link href='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.min.css' rel='stylesheet'>
  <script src='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.js'></script>
  <!-- Import jQuery -->
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
  <!-- Create a container for the map -->
  <div id='map'></div>

  <script>
    // Add your Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-77.0369,38.895], // Specify the starting position
      zoom: 11.5, // Specify the starting zoom
    });
  </script>
</body>

</html>
```

这些代码创建了页面的整体结构，同时在页面的`<head>`中引入了Mapbox GL JS, Assembly, 和 jQuery。Mapbox GL JS 的JavaScript 和 CSS文件让你可以使用 Mapbox GL JS 功能和地图样式，Assembly CSS框架让你可以更多的重定义页面上非地图元素的样式。Jqury 让你可以使用 [Ajax](https://api.jquery.com/jquery.ajax/) 来调用你的等时线API。


页面的 `<body>` 中有一个带有 `map` ID的 `<div>` 元素，这个 `<div>` 元素是地图在页面中展示所在的容器。

保存你的修改，打开 HTML 文件在你的浏览器中可以看到，以Mapbox总部所在的华盛顿哥伦比亚特区为中心创建的地图。

{{
<AppropriateImage imageId="isochroneRenderedMap" alt="Screenshot showing a Mapbox GL JS map rendered in the browser" />
}}

## 添加侧边栏

接下来，添加给web app添加一个侧边栏，来使用户可以选择交通方式和耗时。

在你的HTML页面的 `<body>` 里， 添加一个新的 `<div>`。 这个 `<div>` 保存着app的选项和用户定义样式的 Assembly classes。      

{{<Note title="Using Assembly to style your app" imageComponent={<BookImage />}>}}
这段代码是使用了为特定元素提供CSS样式的[Assembly classes](https://labs.mapbox.com/assembly/) 例如，将`absolute fl my24 mx24 py24 px24 bg-gray-faint round`类应用到当前 `div` 将其定位方式设置为 `absolute` 并将其放在左侧，设置内外边框的宽度为24像素，将背景颜色设置为亮灰色，将边线的转角设置为一定半径的圆形。在你自己的app中，你也可以不使用 Assembly，而使用原生CSS或者你选择的CSS框架，来定义侧边栏和按钮样式。
{{</Note>}}

```html
<div class='absolute fl my24 mx24 py24 px24 bg-gray-faint round'>
  <form id='params'>
    <h4 class='txt-m txt-bold mb6'>Chose a travel mode:</h4>
    <div class='mb12 mr12 toggle-group align-center'>
      <label class='toggle-container'>
        <input name='profile' type='radio' value='walking'>
        <div class='toggle toggle--active-null toggle--null'>Walking</div>
      </label>
      <label class='toggle-container'>
        <input name='profile' type='radio' value='cycling' checked>
        <div class='toggle toggle--active-null toggle--null'>Cycling</div>
      </label>
      <label class='toggle-container'>
        <input name='profile' type='radio' value='driving'>
        <div class='toggle toggle--active-null toggle--null'>Driving</div>
      </label>
    </div>
    <h4 class='txt-m txt-bold mb6'>Chose a maximum duration:</h4>
    <div class='mb12 mr12 toggle-group align-center'>
      <label class='toggle-container'>
        <input name='duration' type='radio' value='10' checked>
        <div class='toggle toggle--active-null toggle--null'>10 min</div>
      </label>
      <label class='toggle-container'>
        <input name='duration' type='radio' value='20'>
        <div class='toggle toggle--active-null toggle--null'>20 min</div>
      </label>
      <label class='toggle-container'>
        <input name='duration' type='radio' value='30'>
        <div class='toggle toggle--active-null toggle--null'>30 min</div>
      </label>
  </form>
</div>
```

这段代码以及应用到其中的 Assembly 类创建了一个的侧边栏，其中有用户可以选择他们所想要的交通方式（步行、骑自行车或者开车）和需要花费的时间（10,20或者30分钟）的控件。

保存你的工作，并且刷新页面。侧边栏将会在页面的左侧展示出来。虽然看起来没什么问题，但点击按钮并不会有任何反应 &mdash; 至少现在没有。下一步，你将添加一个等时线API的调用，这样你就可以将其传递到用户界面，创建一个交互的app。


{{
<AppropriateImage imageId="isochroneAddSidebar" alt="Screenshot showing a sidebar with buttons for driving profiles and trip durations" />
}}

## 添加等时线API

你需要写一个新的函数，来将等时线API集成到你的app中。`getIso`，将会构建查询的字符串，并且使用Ajax来调用等时线API。在你使用 `map` 变量初始化地图后，将下面的代码添加到你的 JavaScript 中。


```js
// // Create variables to use in getIso()
var urlBase = 'https://api.mapbox.com/isochrone/v1/mapbox/';
var lon = -77.034;
var lat = 38.899;
var profile = 'cycling';
var minutes = 10;

// Create a function that sets up the Isochrone API query then makes an Ajax call
function getIso() {
  var query = urlBase + profile + '/' + lon + ',' + lat + '?contours_minutes=' + minutes + '&polygons=true&access_token=' + mapboxgl.accessToken;

  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    console.log(data);
  })
};

// Call the getIso function
// You will remove this later - it's just here so you can see the console.log results in this step
getIso();
```

当你还没有将用来绘制响应中描述的等时线的图层添加到地图中时候，这段代码会将查询的结果打印在控制台。保存你的工作并且刷新页面，打开你的浏览器开发工具仪表。你将会看到等时线API响应对象被打印在了控制台。

{{
<AppropriateImage imageId="isochroneConsoleLog" alt="Screenshot showing the results of the Isochrone API request logged to the console" />
}}

## 绘制等时圈

在最后一步中，你使用 `console.log` 语句来查看API的响应结果。但是在这个app中，你想要将等时圈绘制在地图上！在 Mapbox GL JS 中实现此效果，你需要设置一个新的 _source_ 和 一个新的  _layer_。在 Mapbox GL JS 的文档中获取更多有关 [`addSource`](https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource) 和 [`addLayer`](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer) 方法的信息。

从你的 JavaScript 代码底部移除 `getIso();` 并将其替换成如下的代码：

```js
map.on('load', function() {
 // When the map loads, add the source and layer
 map.addSource('iso', {
   type: 'geojson',
   data: {
     'type': 'FeatureCollection',
     'features': []
   }
 });

 map.addLayer({
   'id': 'isoLayer',
   'type': 'fill',
   // Use "iso" as the data source for this layer
   'source': 'iso',
   'layout': {},
   'paint': {
     // The fill color for the layer is set to a light purple
     'fill-color': '#5a3fc0',
     'fill-opacity': 0.3
   }
 }, "poi-label");

 // Make the API call
 getIso();
});
```

接下来将 `getIso` 函数中的 `console.log(data)` 语句替换为如下的代码，这些代码会将 `iso` 源设置到API返回的数据中。

```js
// Set the 'iso' source's data to what's returned by the API query
map.getSource('iso').setData(data);
```

保存你的更改，并且在浏览器中刷新页面。可手动设置参数（`cycling` 交通方式 和 10 minutes 的耗时）的等时线图，将被绘制在地图中。


{{
<AppropriateImage imageId="isochroneDrawContour" alt="Screenshot showing the isochrone contour drawn on the map" />
}}

## 使 App 可交互
现在，你需要提前把按钮绑定到你的JavaScript, 以便于用户可以改变交通方式与旅行耗时，并且可以在地图中看到结果。在你的 JavaScript 的底部添加如下代码，在 `</script>` 标签前。


```js
// Target the "params" form in the HTML portion of your code
var params = document.getElementById('params');

// When a user changes the value of profile or duration by clicking a button, change the parameter's value and make the API query again
params.addEventListener('change', function(e) {
  if (e.target.name === 'profile') {
    profile = e.target.value;
    getIso();
  } else if (e.target.name === 'duration') {
    minutes = e.target.value;
    getIso();
  }
});
```

现在，当你点击按钮，改变交通方式或者移动耗时，时间监听器在请求中设置新的参数，并且重新运行 `getIso` 函数。这将在地图中重新绘制新的等时线。

保存你的改变并在浏览器中重新刷新页面。点击不同的交通方式和移动耗时组合，来观察等时线的改变。

{{
<AppropriateImage imageId="isochroneChangeProfile" alt="Screenshot showing the isochrone contour has changed when the routing profile and duration buttons are used" />
}}

## 添加一个标记

作为最后一步，你将在你的地图中，请求的坐标处添加一个标记，这样会让等时圈的中心更加明显。在此例子中，这对坐标被设置在了华盛顿哥伦比亚特区的Mapbox的办公室。

将下列的代码添加到你的 JavaScript 中，在 `map.on('load')` 前：

```js
var marker = new mapboxgl.Marker({
 'color': '#314ccd'
});

// Create a LngLat object to use in the marker initialization
// https://docs.mapbox.com/mapbox-gl-js/api/#lnglat
var lngLat = {
 lon: lon,
 lat: lat
};
```
当地图加载好后，将标记点绘制到地图上，将下列代码添加到你的 `map.on('load')` 中：

```js
// Initialize the marker at the query coordinates
marker.setLngLat(lngLat).addTo(map);
```

现在，当你保存你的工作，并且刷新页面，你将在特殊的坐标处看到一个蓝色的标记。


{{
<AppropriateImage imageId="isochroneFinalProduct" alt="Screenshot showing a map with an isochrone contour and a marker at the query coordinates" />
}}

## 最终产品

你已经使用Mapbox的等时圈API创建了一个app，来可视化人可以在给定的时间内走、骑车或者开车走多远。


{{
 <DemoIframe src="/help/demos/get-started-isochrone-api/index2.html" />
}}

最终的HTML文件将看起来如下：


```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Isochrone API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- Import Assembly -->
  <link href='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.min.css' rel='stylesheet'>
  <script src='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.js'> </script>
  <!-- Import jQuery -->
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
  <!-- Create a container for the map -->
  <div id='map'></div>

  <!-- Create a sidebar with buttons for each option -->
  <div class='absolute fl my24 mx24 py24 px24 bg-gray-faint round'>
    <form id='params'>
      <h4 class='txt-m txt-bold mb6'>Chose a travel mode:</h4>
      <div class='mb12 mr12 toggle-group align-center'>
        <label class='toggle-container'>
          <input name='profile' type='radio' value='walking'>
          <div class='toggle toggle--active-null toggle--null'>Walking</div>
        </label>
        <label class='toggle-container'>
          <input name='profile' type='radio' value='cycling' checked>
          <div class='toggle toggle--active-null toggle--null'>Cycling</div>
        </label>
        <label class='toggle-container'>
          <input name='profile' type='radio' value='driving'>
          <div class='toggle toggle--active-null toggle--null'>Driving</div>
        </label>
      </div>
      <h4 class='txt-m txt-bold mb6'>Chose a maximum duration:</h4>
      <div class='mb12 mr12 toggle-group align-center'>
        <label class='toggle-container'>
          <input name='duration' type='radio' value='10' checked>
          <div class='toggle toggle--active-null toggle--null'>10 min</div>
        </label>
        <label class='toggle-container'>
          <input name='duration' type='radio' value='20'>
          <div class='toggle toggle--active-null toggle--null'>20 min</div>
        </label>
        <label class='toggle-container'>
          <input name='duration' type='radio' value='30'>
          <div class='toggle toggle--active-null toggle--null'>30 min</div>
        </label>
    </form>
  </div>

  <script>
    // Add your Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-77.0369, 38.895], // Specify the starting position
      zoom: 11.5, // Specify the starting zoom
    });

    // Create variables to use in getIso()
    var urlBase = 'https://api.mapbox.com/isochrone/v1/mapbox/';
    var lon = -77.034;
    var lat = 38.899;
    var profile = 'cycling';
    var minutes = 10;

    // Create a function that sets up the Isochrone API query then makes an Ajax call
    function getIso() {
      var query = urlBase + profile + '/' + lon + ',' + lat + '?contours_minutes=' + minutes + '&polygons=true&access_token=' + mapboxgl.accessToken;

      $.ajax({
        method: 'GET',
        url: query
      }).done(function(data) {
        // Set the 'iso' source's data to what's returned by the API query
        map.getSource('iso').setData(data);
      })
    };

    var marker = new mapboxgl.Marker({
      'color': '#314ccd'
    });

    // Create a LngLat object to use in the marker initialization
    // https://docs.mapbox.com/mapbox-gl-js/api/#lnglat
    var lngLat = {
      lon: lon,
      lat: lat
    };

    map.on('load', function() {
      // When the map loads, add the source and layer
      map.addSource('iso', {
        type: 'geojson',
        data: {
          "type": 'FeatureCollection',
          "features": []
        }
      });

      map.addLayer({
        'id': 'isoLayer',
        'type': 'fill',
        // Use "iso" as the data source for this layer
        'source': 'iso',
        'layout': {},
        'paint': {
          // The fill color for the layer is set to a light purple
          'fill-color': '#5a3fc0',
          'fill-opacity': 0.3
        }
      }, "poi-label");

      // Initialize the marker at the query coordinates
      marker.setLngLat(lngLat).addTo(map);

      // Make the API call
      getIso();
    });

    // Target the "params" form in the HTML portion of your code
    var params = document.getElementById('params');

    // When a user changes the value of profile or duration by clicking a button, change the parameter's value and make the API query again
    params.addEventListener('change', function(e) {
      if (e.target.name === 'profile') {
        profile = e.target.value;
        getIso();
      } else if (e.target.name === 'duration') {
        minutes = e.target.value;
        getIso();
      }
    });
  </script>
</body>

</html>
```

## 下一步

如果想熟练的掌握这篇教程中所使用到的工具和技术，可以拓展学习以下的资源：

- 学习更多关于如何更好的使用等时圈API，可选择参数如何影响在响应对象中获取的内容，可参阅 [Isochrone API documentation](https://docs.mapbox.com/api/navigation/#isochrone).
- 学习更多关于使用 Mapbox GL JS 在地图中添加图层请参阅 [Add a GeoJSON line example](https://docs.mapbox.com/mapbox-gl-js/example/geojson-line/) 和 [`addLayer` documentation](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer).
