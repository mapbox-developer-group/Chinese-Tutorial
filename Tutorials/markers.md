---
title: Add custom icons or markers
description: You can add markers, style them, and add tooltips dynamically with Mapbox GL JS. This overview samples all the ways to add custom, interactive markers.
thumbnail: markers
level: 1
topics:
- web apps
language:
- Varies
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { LegacyNote } from '../../components/legacy-note';"
contentType: tutorial
---

在 Mapbox Studio 中，设计点数据的样式有很多种不同的方法，[Mapbox Studio](https://www.mapbox.com/studio), [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api/)，Mapbox [iOS](https://www.mapbox.com/ios-sdk) 和 [Android](https://www.mapbox.com/android-sdk) SDKs。本指南将介绍几种方法，通过拥有自定义图标和标记功能的平台，可视化你的点数据。创建自己的地图不只有一种正确的方法，本指南是为了给你提供一个更好的理解，关于哪种方式更契合你的项目。


## 使用 marker playground

使用 [marker playground](/help/interactive-tools/marker-playground/) 在地图上增加一张图片标记，查看必要的平台专属代码，在你的 iOS、Android 或者web 应用上重新创建地图。

![screenshot of the marker playground](/help/img/interactive-tools/marker-playground.png)

## 在 Mapbox GL JS 中添加 markers

如果你已经拥有想要可视化的 GeoJSON 数据，你可以使用 Mapbox GL JS 为你的地图添加自定义标记。在使用M apbox GL JS 标记方法时，你可以使用任何能作为  [image in CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/image) 使用的文件格式，作为你的地图的标记。在 Mapbox GL JS 中完整地创建自定义标记的地图，请参考 [Add custom markers in Mapbox GL JS](/help/tutorials/custom-markers-gl-js/) 教程。此教程是基于代码的。

{{
  <DemoIframe src="/help/demos/custom-markers-gl-js/index.html" />
}}

## 在 Mapbox Studio 中添加自定义图标

如果你开始的时候一团乱麻，需要整理添加到地图中的数据，那请先查看 [Add points to a map](/help/tutorials/add-points-pt-1/) 教程。在本系列教程中，你将会学习如何在 Mapbox Studio 的数据库编辑器中整理有用的数据，在 Mapbox 样式编辑器中给地图增加自定义图标，使用 Mapbox GL JS 添加你的地图的可交互性。添加地图的可交互性，需要编写代码。

{{<img src='/help/img/studio/add-points-preview.gif' alt='animation of points in the dataset editor and custom icons in the style editor' style={{ width: "50%" }} className='fr-mm w-full w360-mm pl24-mm' />}}

### 第一步：创建数据集
在Mapbox数据库编辑器中学习如何创建新的数据库，添加新的点、保存你的数据库和将它输出为切片集。 **[Add points to a web map, Part 1: create a dataset {{<Icon name='arrow-right' inline={true} />}}](/help/tutorials/add-points-pt-1)**

### 第二步：创建样式

学习从 Mapbox 默认样式中创建一个新的样式，添加一个切片集作为一个图层，在 Mapbox 样式编辑器中使用自定义图标设计点样式。 **[Add points to a web map, Part 2: create a style {{<Icon name='arrow-right' inline={true} />}}](/help/tutorials/add-points-pt-2)**

### 第三步：添加可交互性

学习使用M apbox GL JS 为每个被点击的点增加弹出窗口。这部分需要编写代码。 **[Add points to a web map, Part 3: add interactivity {{<Icon name='arrow-right' inline={true} />}}](/help/tutorials/add-points-pt-3)**

{{
  <Note
    imageComponent={<BookImage />}
  >
    <p>In this tutorial series you will add custom icons inside Mapbox Studio. Mapbox Studio only supports SVG images. Other image formats are supported when using markers in Mapbox GL JS.</p>
  </Note>
}}

## 在iOS中添加标记

IOS 版的 Mapbox 地图软件开发包（The Mapbox Maps SDK for iOS）为可视化地图上的点数据提供了一系列不同的方式。每种方法各有利弊，所以当你需要添加大量图标或者显示高度自定义图标时，务必扫一眼。

请查看面向 The Mapbox Maps SDK for iOS 的 [Adding Points to a Map](https://www.mapbox.com/ios-sdk/maps/overview/markers-and-annotations/) 指南，以获取更多信息，关于如何使用有效的方法可视化你地图上的点数据，并权衡每种方法的利弊。

## 在 Android 中添加标记

在使用 Android 版的地图软件工具包给地图添加标记时，我们推荐注释插件 [Annotation plugin](https://docs.mapbox.com/android/plugins/overview/annotation) 。注释插件简化了在 Mapbox map 上设置和调整注释的可视属性的方法。

[Directly using the Maps SDK for Android's sources and layers](https://docs.mapbox.com/android/maps/overview/data-driven-styling/) 是比注释插件更加先进的添加注释的方法。


## 在 Mapbox.js 中添加标记

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Add custom markers in Mapbox GL JS',
      link: '/help/tutorials/custom-markers-gl-js/'
    }}
  />
}}

如果你想了解如何使用 Mapbox.js 添加标记，阅读我们的 [Work with markers with Mapbox.js](/help/tutorials/markers-js) 指南。在这个指南中，你将会学习如何添加标记、自定义它们，并用 [Mapbox.js](https://www.mapbox.com/mapbox.js) 使它们变得可交互。

