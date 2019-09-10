---
title: Spatial analysis
description: Learn how spatial analysis with Turf works and how to use Turf in your web application.
image: /img/narrative/analysis.svg
topics:
  - analysis
prependJs:
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: guide
---
标题：空间分析

描述：学习如何使用Turf进行空间分析以及如何在Web应用程序中使用Turf

Spatial analysis includes a variety of techniques and processes used to understand the patterns and relationships of geographic features. [Turf](http://turfjs.org/) is an advanced geospatial JavaScript open source library that allows you to do spatial operations in the browser. Turf helps you analyze, aggregate, and transform data to visualize it in new ways and answer advanced questions. This guide provides an overview of how spatial analysis with Turf works, how to use Turf in your application, and relevant documentation to help you get started.

空间分析包含用于理解地理学特征的模式和关系的各种技术和过程。[Turf](http://turfjs.org/)是一个允许你在浏览器中执行空间操作的高级地理空间JavaScript开源库。Turf帮助你分析、聚合和转换数据，以便以新的可视化方式呈现，并解答一些高级进阶的问题。这篇教程概述了如何使用Turf进行空间分析，如何在应用程序中使用Turf，以及相关的文档来帮助你入门。

<div class='bg-white border-b'>
  <div class='txt-m txt-bold'>Perform spatial operations in the browser</div>
  <div class='txt-xs pb6'>Click points on the map to create lines that measure distanced using turf.lineDistance.</div>
</div>

{{
  <DemoIframe src="/help/demos/how-mapbox-works/spatial-analysis.html" />
}}

<div class='bg-white border-b'>
  <div class='txt-m txt-bold'>在浏览器中执行空间分析</div>
  <div class='txt-xs pb6'>点击地图上的点画线并用turf.lineDistance.来测量线的距离</div>
</div>

{{
  <DemoIframe src="/help/demos/how-mapbox-works/spatial-analysis.html" />
}}

## How spatial analysis works

[Turf](http://turfjs.org/) is a library for **geospatial analysis** &mdash; a large family of tasks like _calculating area and distance_ and _joining points to polygons_ that enable people to see patterns or relationships within their data. Spatial analysis is used in many industries: to find the [nearest coffee shop](https://www.mapbox.com/blog/coffee-with-turf/), [calculate travel time](https://www.mapbox.com/blog/playback-the-iditarod-with-turf/), and show [regional statistics for utility usage](https://www.mapbox.com/blog/turf-government-data/). It's also a huge part of GIS, where many problems are solved with spatial analysis.

## 如何进行空间分析
[Turf](http://turfjs.org/)是一个**空间分析库** &mdash;一系列大型的任务，比如_计算面积和距离_和_将点连接成多边形_使人们能到看到数据中的模式和关系。空间分析可用在很多行业中：查找[最近的咖啡店](https://www.mapbox.com/blog/coffee-with-turf/)，[计算出行时间](https://www.mapbox.com/blog/playback-the-iditarod-with-turf/)，并展示[公用事业的区域统计数据](https://www.mapbox.com/blog/turf-government-data/)。空间分析也是GIS的重要组成部分，许多问题都是通过空间分析解决的。


### Examples of spatial analysis

<div class='fr pl12' style='width:50%'>
  <img alt='map of 1854 cholera outbreak in London' src='/help/img/screenshots/snow-cholera-map-1.jpg' />
  <p class='caption'><strong>Source</strong>: John Snow - Published by C.F. Cheffins, Lith, Southhampton Buildings, London, England, 1854 in Snow, John. On the Mode of Communication of Cholera, 2nd Ed, John Churchill, New Burlington Street, London, England, 1855.</p>
</div>

### 空间分析的案例

<div class='fr pl12' style='width:50%'>
  <img alt='1854年伦敦霍乱爆发图' src='/help/img/screenshots/snow-cholera-map-1.jpg' />
  <p class='caption'><strong>Source</strong>: John Snow - Published by C.F. Cheffins, Lith, Southhampton Buildings, London, England, 1854 in Snow, John. On the Mode of Communication of Cholera, 2nd Ed, John Churchill, New Burlington Street, London, England, 1855.</p>
</div>

The map below is a classic example of spatial analysis, created by physician John Snow during the 1854 cholera outbreak in London. Snow [plotted](http://en.wikipedia.org/wiki/1854_Broad_Street_cholera_outbreak) cholera cases in the Soho area of London around Broad Street and noticed a cluster around the water pump. This led to improved sanitation facilities and the discovery that cholera infection was water-borne rather than airborne.

下图是一个典型的空间分析的案例，由医生John Snow绘制于1854年轮渡霍乱爆发时期。 Snow[绘制](http://en.wikipedia.org/wiki/1854_Broad_Street_cholera_outbreak)在伦敦Broad街Soho区域的霍乱病例，注意到水泵周边有一个聚集区。 这个结果促进改善了卫生设施，并发现霍乱感染是由水传播而非空气传播。

Today, spatial analysis is used in epidemiology, biology, statistics, economics, commerce and business, urban planning, geology, oil and gas, and in [many other industries](https://www.mapbox.com/industries/). With Turf, we can now bring these analyses to the browser and show results quickly and seamlessly.

今天，空间分析被用在流行病学，生物学，统计学，经济学，商业和商业，城市规划，地质学，石油和天然气，以及[许多其他行业](https://www.mapbox.com/industries/)。使用Turf，我们现在可以将这些分析向浏览者快速无缝地显示结果。

### Common functions

There are dozens of functions available within Turf that allow you to do spatial operations with your data. Some of the most common operations are:

- **Buffer**: returns an area that is a specified number of units around your feature.
- **Inside**: returns whether a feature is wholly within an area.
- **Area**: calculates the area of a polygon.
- **Along**: returns the position of a point at a specified distance along a line.

### 常用功能

Turf中有许多可用的功能，允许你对数据进行空间操作。 一些最常见的操作是：

- **缓冲区Buffer**: 目标周围指定单位数的区域。
- **内部Inside**: 目标是否完全在某个范围内。
- **面积Area**: 计算一个多边形的面积。
- **沿着Along**: 沿着一条线指定距离的点的位置。

A typical Turf operation such as the **buffer** function would look like this in JavaScript:

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

一个典型的Turf操作，比如 **buffer** 函数在JavaScript中是这样的：

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


### Method types

There are several different kinds of spatial analysis you can conduct with Turf. All Turf methods are organized into the following categories:

### 方法类型

你可以使用Turf进行多种不同类型的空间分析。 Turf所有的方法可分为以下几类：

- **Aggregation methods** can run statistical operations on a set of points within a set of polygons. For example, you can compare average size of elementary schools across counties in Massachusetts with [turf-collect](http://turfjs.org/docs#collect).

- **集合方法Aggregation methods** 统计一组多边形内点的集合。比如，你可以用[turf-collect](http://turfjs.org/docs#collect)比较Massachusetts各县小学的平均规模。

- **Measurement methods** can measure distances, create features, and calculate sizes. For example, with measurement methods, you can determine not only the exact center point of the city of Austin (with [turf-centroid](http://turfjs.org/docs#centroid), but you can also measure the distance between that point and city hall (with [turf-distance](http://turfjs.org/docs#distance)).

- **测量方法Measurement methods** 可以测量距离，新建特征，和计算大小。比如，使用测量方法，您不仅可以确定Austin市的确切中心点（使用[turf-centroid](http://turfjs.org/docs#centroid)，还可以测量那个点和市政厅之间的距离（[turf-distance](http://turfjs.org/docs#distance))。

- **Transformation methods** can solve spatial problems. If you want to buy a house that is both within one mile of a park and one mile of a bus stop, you can determine where those areas overlap with [turf-intersect](http://turfjs.org/docs#intersect), a transformation method.

- **转换方法Transformation methods** 用来解决空间问题。如果你需要购买同时距离公园和公交站内一英里范围内的房子，你可以用转换方法中[turf-intersect](http://turfjs.org/docs#intersect)发现这些叠加的区域。

- **Data methods** can generate random points or samples from a large number of features *at random*. For example, you can use [turf-sample](http://turfjs.org/docs#sample) to list a subset of store locations from hundreds of locations.

- **数据方法Data methods**可以从*随机*的大量特征中形成随机点或样本。比如，使用[turf-sample](http://turfjs.org/docs#sample)从数百的位置数据中列出子系列-商店的位置。

- **Interpolation methods** can estimate or average data and visualize the result. For example, creating contour lines (or isobands) from a set of points containing elevation information with [Turf isobands](http://turfjs.org/docs#isolines).

- **差值方法Interpolation methods** 可以估算或计算数据的平均值，并可视化结果。比如，用[Turf isobands](http://turfjs.org/docs#isolines)从包含高程信息的一组点来新建等高线（等边线）

- **Join methods** can determine spatial relationships between features. If you want to know which burglaries happened in a specific neighborhood, you can use a join method like [turf-within](http://turfjs.org/docs#within).

- **连接方法Join methods** 可以确定要素之间的空间关系。如果你想知道在特定街区发生了哪些盗窃案，你可以使用连接方法中的 [turf-within](http://turfjs.org/docs#within)。


## Using spatial analysis

As a JavaScript library, you can add [Turf](http://turfjs.org/) to your webpage in the `<head>` of your document. You can use the CDN (the URL displayed below), or you can [download the Turf library](http://turfjs.org/) and source it locally.

```html
<script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
```

## 使用空间分析

作为JavaScript库，你可以添加[Turf](http://turfjs.org/)到你网页文档的 `<标题>` 处。 您可以使用CDN（下面显示的URL），也可以[下载 Turf库](http://turfjs.org/) 并作为本地资源。

```html
<script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
```

When you add Turf to your site, it exposes a global variable `turf` from which you can run any of the [turf functions](http://turfjs.org/docs). For example, if you have a GeoJSON LineString feature named `dc` and you want to know its length in miles, you can use the [turf-length](http://turfjs.org/docs#length) function.

当你加载Turf到自己的模块，它会出现一个通用的变量`turf`，你可以从中运行任何[turf模块](http://turfjs.org/docs)。比如，如果你有一个名为`dc`的GeoJSON LineString要素, 你可以使用[turf-length](http://turfjs.org/docs#length)函数来计算它长度的英里数。

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

The variable `length` contains the length of `dc` in miles.

 `length`变量包含`dc` 长度的英里数。

```js
// length === 1.6389817168470033
```

You can find a complete list of available functions and see them in action in the [Turf API documentation](http://turfjs.org/docs).

你可以在[Turf API documentation](http://turfjs.org/docs)找到所有可用函数的完整列表和操作方法。

