---
title: 使用 Mapbox GL JS 显示数据随时间的变化
description: 用 MapBox GL JS 创建一个地图应用来显示数据随时间而变化。
thumbnail: showDataChangeOverTime
level: 3
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
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

{{
  <Note
    imageComponent={<BookImage />}
    title='属性函数 vs. 属性表达式'

  >
  >    <p>这个教程使用了属性<em>表达式</em>。这个新特性是在 <a href='https://github.com/mapbox/mapbox-gl-js/blob/master/CHANGELOG.md#0410-october-11-2017'>Mapbox GL JS v0.41.0</a>引入的。属性<em>表达式</em>能帮你完成属性<em>函数</em>相似的效果，但有更多的灵活性和功能。<strong>任何<a href='https://www.mapbox.com/mapbox-gl-js/style-spec#other-function'>属性函数</a>出现的地方，它们最终被弃用而由属性表达式所替代，</strong></p>
  >    <p>在 <a href='https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions'>Mapbox Style Specification</a> 和 <a href='/help/tutorials/mapbox-gl-js-expressions/'>Get started with Mapbox GL JS expressions</a> 读取更多关于表达式的内容。</p>
  >  </Note>
  >}}

这个教程将展示如何使用 [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/) 创建一个显示数据随时间变化的地图。在这个向导中你会用到的源数据来自 [NYC OpenData](https://data.cityofnewyork.us/)，它包含了2016年1月纽约市发生的15000起交通事故。

如果你刚开始接触 Mapbox GL JS 的话，你可能想要先读读 [Mapbox GL JS fundamentals](/help/how-mapbox-works/web-apps/)。

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-final.html" />
}}

## 开始教程

开始之前你需要一些资源：

- [**An access token**](/help/glossary/access-token/) 来自你的 Mapbox 账号。这个访问口令是用来关联你的地图和你的账户，你能在你的[Account page](https://www.mapbox.com/account)找到。
- **Data**。这个GeoJSON文件包含了2016年1月份的15273起含地理信息编码的交通事件，下载于 [NYC OpenData](https://data.cityofnewyork.us/Public-Safety/NYPD-Motor-Vehicle-Collisions/h9gi-nx95) 。
{{<Button href="/help/data/collisions1601.geojson" passthroughProps={{ download: "collisions1601.geojson" }}>
    <Icon name='arrow-down' inline={true} />下载数据</Button>}}
- **A text editor** 用来写 HTML，CSS 和 JavaScript。

## 添加地图

在你开始增加 NYC 交通事件数据前，你需要先创建一个地图来放置它们。首先创建一个 HTML 文件，然后在这个页面初始化地图对象。这个教程将需要几个文件，因此我们推荐在你的电脑上创建一个工程文件夹来一起存放它们。

### 创建 HTML 文件

在你的工程文件夹下，创建一个 `index.html` 文件。增加 Mapbox GL JS and CSS 到HTML文档的 `head` 中。

```html
<meta charset='utf-8' />
<title>NYC motor vehicle collisions</title>
<meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
<script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

然后，创建一个地图容器和一个用于图例和数据交互控件的容器，添加它们到 HTML 文档的 `body` 中。

```html
<div id='map'></div>
<div id='console'>
  <h1>Motor vehicle collisions</h1>
  <p>Data: <a href='https://data.cityofnewyork.us/Public-Safety/NYPD-Motor-Vehicle-Collisions/h9gi-nx95'>Motor vehicle collision injuries and deaths</a> in NYC, Jan 2016</p>
</div>
```

使用 CSS 创建页面排版布局。在 `head` 之后创建一对 `style` 标签，再增加如下代码：

```css
body {
  margin: 0;
  padding: 0;
  font-family: 'Helvetica Neue', Helvetica, Arial, Sans-serif;
}

#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}

h1 {
  font-size: 20px;
  line-height: 30px;
}

h2 {
  font-size: 14px;
  line-height: 20px;
  margin-bottom: 10px;
}

a {
  text-decoration: none;
  color: #2dc4b2;
}

#console {
  position: absolute;
  width: 240px;
  margin: 10px;
  padding: 10px 20px;
  background-color: white;
}
```

### 初始化地图

一旦你完成了页面结构，你就能用 Mapbox GL JS 初始化一个地图了。 在 `body` 结尾处增加一对 `script` 标签 &mdash; 你将写所有下面的代码(JavaScript)到这两个 `script` 标签之间。

首先用 `new mapboxgl.Map()` 创建一个新的 `map` 对象，然后将它存储到一个叫 `map` 的变量中。

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

var map = new mapboxgl.Map({
  container: 'map', // container element id
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  center: [-74.0059, 40.7128], // initial map center in [lon, lat]
  zoom: 12
});
```

如果你启动了页面，它应该看起来这样：

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-one.html" />
}}

## 加载数据

一旦你的页面结构和地图完成并添加到页面后，接下来要加载你的数据了，样式化，添加图例。幸运地，Mapbox GL JS 有一些易用的函数可以帮助使用！ 首先， 确保你下载的 `collisions1601.geojson` 文件在你的工程文件夹下。

### 添加图层

为了用 Mapbox GL JS 添加数据到你的地图，你需要创建一个包含 [source](/help/glossary/source) 的 [layer](/help/glossary/layer) 。 在这个例子中， 你将使用你之前下载的 GeoJSON 文件作为你地图的数据源。

{{
  <Note
    imageComponent={<BookImage />}
  >
  >    <p>确保存储和部署的 GeoJSON 文件和你的工程在同一个域内。你也将需要从一个本地Web服务器下运行这个应用，否则你将收到一个 <a href='http://en.wikipedia.org/wiki/Cross-origin_resource_sharing'>跨域资源共享 (CORS)</a>错误。 <a href='http://www.2ality.com/2014/06/simple-http-server.html'>Python's SimpleHTTPServer</a> 在很多计算机上都包含，如果这是你第一次运行本地服务器，用它就是一个不错的选择。</p>
  >  </Note>
  >}}

在这个例子中，你将使用 [expressions](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions) 根据数据中的属性设置点的样式。这种 [data-driven styling](/help/glossary/data-driven-styling) 方式允许您为地图可视化添加额外的维度，帮助向读者传达特定的见解或信息。
在这种情况下，可以通过应用基于数据中的 `Casualty` 财产（即碰撞中受伤或死亡的总人数）的样式，使地图更具信息性。下面的代码将根据 `Casualty` 区域更改点的大小和颜色。

下面使用的两个表达式都是 [`'interpolate'`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-interpolate) 表达式。这种表达式在输入和输出值对之间连续插值。在这种情况下，'linear' 插值可用于 `circle-radius` 和 `circle-color`，以确保插值在两个停止点之间平滑、线性地进行。

另外，注意 `map.on('load', function(){} )`下面的代码 — 它告诉你的浏览器必须要要等你的地图加载完成后才能添加新其他东西。任何关于添加图层的代码都应该放到这个回调函数内部。

```js
map.on('load', function() {
  map.addLayer({
    id: 'collisions',
    type: 'circle',
    source: {
      type: 'geojson',
      data: './collisions1601.geojson' // replace this with the url of your own geojson
    },
    paint: {
      'circle-radius': [
        'interpolate',
        ['linear'],
        ['number', ['get', 'Casualty']],
        0, 4,
        5, 24
      ],
      'circle-color': [
        'interpolate',
        ['linear'],
        ['number', ['get', 'Casualty']],
        0, '#2DC4B2',
        1, '#3BB3C3',
        2, '#669EC4',
        3, '#8B88B6',
        4, '#A2719B',
        5, '#AA5E79'
      ],
      'circle-opacity': 0.8
    }
  });
});

```

### 创建图例

为了描述你增加的数据内容，创建一个图例来说明每个颜色和大小表示的意义。首先用类 `session` 创建一个新的`div` 添加到在你之前加过的 `console` `div`  内。

```html
<div class='session'>
  <h2>Casualty</h2>
  <div class='row colors'>
  </div>
  <div class='row labels'>
    <div class='label'>0</div>
    <div class='label'>1</div>
    <div class='label'>2</div>
    <div class='label'>3</div>
    <div class='label'>4</div>
    <div class='label'>5+</div>
  </div>
</div>
```

接下来，应用一些 CSS 来定义新 `session` 类的样式。使用与在图层中定义的 `circle-color` 值的停止点相同的颜色创建颜色渐变。这应该放在前面添加的 `style` 标记中。

```css
.session {
  margin-bottom: 20px;
}

.row {
  height: 12px;
  width: 100%;
}

.colors {
  background: linear-gradient(to right, #2dc4b2, #3bb3c3, #669ec4, #8b88b6, #a2719b, #aa5e79);
  margin-bottom: 5px;
}

.label {
  width: 15%;
  display: inline-block;
  text-align: center;
}
```

增加完CSS样式后，刷新你的浏览器，你将看到以下页面:

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-two.html" />
}}

## 添加时间滑块

以伤亡为标志的数据，你的地图已经在讲述一个令人信服的故事。为了使其更有吸引力，您可以添加一个时间滑块条，以允许读者按时间过滤交通事故数据。

### 添加地图过滤器

除了给渲染或排版属性提供值之外，你能用表达式作过滤器。通过增加一个 [`==`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-==) 表达式作为过滤器，它结构如
 `"filter": ['==', ['type',['get', 'key']],'value']`，你能找出所有那些 key 等于指定 value 的元素。
增加下面的代码到你之前写的 `addLayer()` 部分的后面：

```
filter: ['==', ['number', ['get', 'Hour']], 12]
```

刷新地图。你应该看到更少的事故!

### 创建一个滑块条

你如果不想仅仅显示中午时段发生的事故，而是你想让你的用户可以控制什么时间的地图数据显示。要做这个，您可以在 `console` 层中添加一个时间滑块，方法是在 `legend` 之后添加一个新的 `session` 层。在数据里有24个时刻被标记为整数0-23，因此，你可以将输入的 `min` 和 `max` 属性分别设置为 `0` 和 `23`，初始值分别设置为12或12PM。增加下面的代码到你前一步添加另一个`session` 层中：

```html
<div class='session' id='sliderbar'>
  <h2>Hour: <label id='active-hour'>12PM</label></h2>
  <input id='slider' class='row' type='range' min='0' max='23' step='1' value='12' />
</div>
```

### 添加交互性

现在增加一些代码来关联滑动条和地图。首先增加一个 `onInput` 事件监听器给滑块条，它将监听滑块条上数值的任何变化。然后，任何时候  `input` 事件被触发, 用 Mapbox GL JS 的 `setFilter(layer, filter)`方法改变你的图层的 `filter` 属性。最后，加一点运算来增加 `PM` 或 `AM` 到显示在滑块旁边的时间。

增加这部分到你的脚本`addLayer()`之后：

```js
document.getElementById('slider').addEventListener('input', function(e) {
  var hour = parseInt(e.target.value);
  // update the map
  map.setFilter('collisions', ['==', ['number', ['get', 'Hour']], hour]);

  // converting 0-23 hour to AMPM format
  var ampm = hour >= 12 ? 'PM' : 'AM';
  var hour12 = hour % 12 ? hour % 12 : 12;

  // update text in the UI
  document.getElementById('active-hour').innerText = hour12 + ampm;
});

```

看起来应该这样：

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-three.html" />
}}

## 按照星期几筛选

另一个收集纽约市交通事故信息的有用指标是事故发生的星期几。使用下面的代码，您可以添加单选按钮来筛选一周中的几天。

### 创建单选按钮组

首先，在你的HTML页面的 `console` 层内，增加下面的单选按钮组：

```html
<div class='session'>
  <h2>Day of the week</h2>
  <div class='row' id='filters'>
    <input id='all' type='radio' name='toggle' value='all' checked='checked'>
    <label for='all'>All</label>
    <input id='weekday' type='radio' name='toggle' value='weekday'>
    <label for='weekday'>Weekday</label>
    <input id='weekend' type='radio' name='toggle' value='weekend'>
    <label for='weekend'>Weekend</label>
  </div>
</div>
```

### 添加交互性

在代码中创建一个新的 `change` 事件监听器，就像对滑块所做的那样，然后将其放置在滑块事件之后。
要显示所有天的碰撞，请使用 [`!=`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-!=) 筛选 “placeholder” 值的表达式。添加此筛选器后，`filterDay` 的计算结果永远不会为空。在本教程结束之前，我们将更加清楚为什么这是必要的。

要筛选工作日和周末值，请使用 `match` 表达式。匹配表达式允许您指定输入和输出值。以下表达式的模式如下：

```
['match', ['get', property], inputValue, outputValue if match, outputValue if not a match]
```

增加下面的代码到你上一步添加的滑动事件的后面 :

```js
document.getElementById('filters').addEventListener('change', function(e) {
  var day = e.target.value;
  // update the map filter
  if (day === 'all') {
    filterDay = ['!=', ['string', ['get', 'Day']], 'placeholder'];
  } else if (day === 'weekday') {
    filterDay = ['match', ['get', 'Day'], ['Sat', 'Sun'], false, true];
  } else if (day === 'weekend') {
    filterDay = ['match', ['get', 'Day'], ['Sat', 'Sun'], true, false];
  } else {
    console.log('error');
  }
  map.setFilter('collisions', ['all', filterDay]);
});
```

刷新你的页面，并尝试点击星期几的按钮。

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-four.html" />
}}

## 组合过滤器 

正如您可能已经发现的，在工作日和周末之间切换将自动覆盖小时筛选器。你可以用组合过滤器 ([documentation](https://www.mapbox.com/mapbox-gl-style-spec/#types-filter)) 来解决这个问题。

### 组合的过滤器

若要组合多个筛选器，请将它们附加到新的表达 [`'all'`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-all) 式中。使用此`'all'`表达式可确保两个筛选器都为true。

在地图 `load` 事件处理程序的开头添加两个变量，以存储“hour”和“day of the week”筛选器并独立应用它们。
这样当你想更新过滤器的一部分时，你可以更新这个变量，然后应用 setFilter(`my layer`, `['all', filterHour, filterDay]`) 来重置过滤器。

首先，在你之前创建的地图 `load` 事件处理前增加两个变量。这是需要占位符筛选器的地方，因为组合筛选器中不能有`null`。

```js
var filterHour = ['==', ['number', ['get', 'Hour']], 12];
var filterDay = ['!=', ['string', ['get', 'Day']], 'placeholder'];
```
其次，在 `addLayer` 里，用 `['all', filterHour, filterDay]` 替换 `filter` 的值。

再次，在滑动条的 `onInput` 事件，用下面代码替换 `map.setFilter('collisions', ['==', ['number', ['get', 'Hour']], hour]);`：

```js
filterHour = ['==', ['number', ['get', 'Hour']], hour];
map.setFilter('collisions', ['all', filterHour, filterDay]);
```
最后，用下面的代码，替换星期几按钮的 `onChange` 事件:

```js
document.getElementById('filters').addEventListener('change', function(e) {
  var day = e.target.value;
  if (day === 'all') {
    // `null` would not work for combining filters
    filterDay = ['!=', ['string', ['get', 'Day']], 'placeholder'];
  }
  /* the rest of the if statement */
  map.setFilter('collisions', ['all', filterHour, filterDay]);
});
```

## 最终产品

你已经创建了一个展示2016年1月份 NYC 交通事故数据的地图，完全采用数据驱动样式，有图例，时间滑动条并且能按照星期几筛选过滤。

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-five.html" />
}}

## 下一步

通过本教程，您可以使用 Mapbox GL JS 创建自己的交互式时间序列数据可视化。在我们的帮助页面上探索更多的 Mapbox GL JS 资源，并查看完整的 [Mapbox GL JS documentation](https://www.mapbox.com/mapbox-gl-js) 文档和 [examples](https://www.mapbox.com/mapbox-gl-js/examples) 示例以获得更多的灵感和指导。
