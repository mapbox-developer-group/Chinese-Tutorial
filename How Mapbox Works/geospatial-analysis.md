---
标题: 空间分析
描述: 学习如何使用Turf进行空间分析以及如何在Web应用程序中使用Turf.
图像: /img/narrative/analysis.svg
主题:
  - 分析
prependJs:
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
文章类别: 教程
---

空间分析包含用于理解地理学特征的模式和关系的各种技术和过程. [Turf](http://turfjs.org/) 是一个允许你在浏览器中执行空间操作的高级地理空间JavaScript开源库. Turf 帮助你分析、聚合和转换数据，以便以新的可视化方式呈现，并解答一些高级进阶的问题. 这篇教程概述了如何使用Turf进行空间分析，如何在应用程序中使用Turf，以及相关的文档来帮助你入门.

<div class='bg-white border-b'>
  <div class='txt-m txt-bold'>在浏览器中执行空间分析</div>
  <div class='txt-xs pb6'>点击地图上的点画线并用 turf.lineDistance来测量线的距离.</div>
</div>

{{
  <DemoIframe src="/help/demos/how-mapbox-works/spatial-analysis.html" />
}}

## 如何进行空间分析

[Turf](http://turfjs.org/)是一个 **空间分析库** &mdash; 一系列大型的任务，比如 _计算面积和距离_ 和 _将点连接成多边形_ 使人们能到看到数据中的模式和关系. 空间分析可用在很多行业中: 查找 [最近的咖啡店](https://www.mapbox.com/blog/coffee-with-turf/), [计算出行时间](https://www.mapbox.com/blog/playback-the-iditarod-with-turf/), 并展示 [公用事业的区域统计数据](https://www.mapbox.com/blog/turf-government-data/). 空间分析也是GIS的重要组成部分，许多问题都是通过空间分析解决的.

### 空间分析的案例

<div class='fr pl12' style='width:50%'>
  <img alt='1854年伦敦霍乱爆发图' src='/help/img/screenshots/snow-cholera-map-1.jpg' />
  <p class='caption'><strong>Source</strong>: John Snow - Published by C.F. Cheffins, Lith, Southhampton Buildings, London, England, 1854 in Snow, John. On the Mode of Communication of Cholera, 2nd Ed, John Churchill, New Burlington Street, London, England, 1855.</p>
</div>

下图是一个典型的空间分析的案例, 由医生 John Snow 绘制于1854年伦敦霍乱爆发时期. Snow [绘制](http://en.wikipedia.org/wiki/1854_Broad_Street_cholera_outbreak) 在伦敦Broad街Soho区域的霍乱病例时注意到水泵周边有一个聚集区. 这个结果促进改善了卫生设施，并发现霍乱感染是由水传播而非空气传播.

今天, 空间分析被用在流行病学, 生物学, 统计学, 经济学, 商业和商务, 城市规划, 地质学, 石油和天然气, 以及 [许多其他行业](https://www.mapbox.com/industries/). 使用 Turf, 我们现在可以将这些分析结果向浏览者快速无缝地显示.

### 常用功能

Turf 中有许多可用的功能，允许你对数据进行空间操作. 一些最常见的操作是:

- **缓冲区Buffer**: 目标周围指定单位数的区域.
- **内部Inside**: 目标是否完全在某个范围内.
- **面积Area**: 计算一个多边形的面积.
- **沿着Along**: 沿着一条线指定距离的点的位置.

一个典型的 Turf 操作比如 **buffer** 函数在 JavaScript中是这样的:

```js
var nullIsland = {
  type: 'Feature',
  geometry: {
    type: 'Point',
    coordinates: [0, 0]
  },
  properties: {
    name: 'Null Island'
  }
};

var twoHundredMilesOut = turf.buffer(nullIsland, 200, { unit: 'miles' });

```

{{
  <DemoIframe src="/help/demos/turf-intro/nullisland.html" />
}}

### 方法类型

你可以使用 Turf进行多种不同类型的空间分析. Turf 所有的方法可分为以下几类:

- **集合方法Aggregation methods** 统计一组多边形内点的集合. 比如, 你可以用 [turf-collect](http://turfjs.org/docs#collect)比较Massachusetts各县小学的平均规模.

- **测量方法Measurement methods** 可以测量距离, 新建特征, 和计算大小. 比如, 使用测量方法, 您不仅可以确定Austin市的确切中心点 (使用 [turf-centroid](http://turfjs.org/docs#centroid), 还可以测量那个点和市政厅之间的距离 (使用 [turf-distance](http://turfjs.org/docs#distance)).

- **转换方法Transformation methods** 用来解决空间问题. 如果你需要购买同时距离公园和公交站内一英里范围内的房子, 你可以用转换方法中[ [turf-intersect](http://turfjs.org/docs#intersect)发现这些叠加的区域, 这时一种转换的方法.

- **数据方法Data methods** 可以从 *随机* 的大量特征中形成随机点或样本. 比如, 使用 [turf-sample](http://turfjs.org/docs#sample) 从数百的位置数据中列出子系列商店的位置.

- **差值方法Interpolation methods** 可以估算或计算数据的平均值，并可视化结果. 比如, 用 [Turf isobands](http://turfjs.org/docs#isolines)从包含高程信息的一组点来新建等高线（等边线）.

- **连接方法Join methods** 可以确定要素之间的空间关系. 如果你想知道在特定街区发生了哪些盗窃案, 你可以使用连接方法中的 [turf-within](http://turfjs.org/docs#within).


## 使用空间分析

作为一个 JavaScript 库, 你可以添加 [Turf](http://turfjs.org/) 到你网页文档的 `<标题>` 处. 你可以使用 CDN (下面显示的 URL), 也可以 [下载 Turf 库](http://turfjs.org/) 并作为本地资源.

```html
<script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
```

当你加载 Turf 到自己的模块, 它会出现一个通用的变量 `turf` 你可以从中运行任何 [turf 模块](http://turfjs.org/docs). 如果你有一个名为 `dc`的GeoJSON LineString要素, 你想知道它长度的英里数, 你可以使用 [turf-length](http://turfjs.org/docs#length) 函数.

```js
var dc = {
  type: 'Feature',
  properties: {},
  geometry: {
    type: 'LineString',
    coordinates: [
      [-77.031669, 38.878605],
      [-77.029609, 38.881946],
      [-77.020339, 38.884084],
      [-77.025661, 38.885821],
      [-77.021884, 38.889563],
      [-77.019824, 38.892368]
    ]
  }
};

var length = turf.length(dc, { units: 'miles' });
```

{{
  <DemoIframe src="/help/demos/turf-intro/linestring.html" />
}}

变量 `length` 包含 `dc` 长度的英里数.


你可以在 [Turf API documentation](http://turfjs.org/docs)找到所有可用函数的完整列表和操作方法.


