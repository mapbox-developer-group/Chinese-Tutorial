---
title: 入门适用于iOS的Mapbox地图SDK中的表达式
description: 创建一个根据数据属性对圆圈设置样式的iOS地图。
thumbnail: iosDdsCircleLayer
level: 2
topics:
- mobile apps
language:
- Swift
- Objective-C
prereq: Familiarity with Xcode and either Swift or Objective-C, and completion of the Mapbox Maps SDK for iOS installation guide.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { IosCodeToggle } from '../../components/ios-code-toggle'"
  - "import * as snippet from '../../snippets/ios-dds-circle-layer.js'"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

在本篇指南中您将学习如何使用适用于iOS的Mapbox地图SDK中的表达式来根据数据属性和缩放级别自定义样式。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-post-zoom-expression.png' alt='adjust the circle radius based on zoom level' /></div>
</div>
}}

## 入门

本指南假设您已经熟悉Objective-C 或者 Swift。以下是在您开始之前需要的资源：

- **一个包含适用于iOS的Mapbox地图SDK的程序。** 本指南还假设您已经使用适用于iOS的Mapbox地图SDK创建了一个 `MGLMapView`。如果您是适用于iOS的Mapbox地图SDK的新手，请先完成[First steps with the Mapbox Maps SDK for iOS](/help/tutorials/first-steps-ios-sdk/) 指南，来创建一个地图视图。
- **数据**。 在本教程中，您将使用[HPC Landmarks from Open Minneapolis](http://opendata.minneapolismn.gov/datasets/hpc-landmarks/data)的CSV文件。

{{
<Button href="/help/data/trees.geojson" passthroughProps={{ download: "trees.geojson" }} >
    <Icon name='arrow-down' inline={true} /> 下载数据
</Button>
}}

## 什么是表达式?

在[Mapbox 样式说明](https://www.mapbox.com/mapbox-gl-js/style-spec/)中，任意布局属性，绘图属性，或者过滤器的值均可指定为表达式。表达式定义如何使用逻辑，数学，字符串或颜色操作符来组合一个或多个要素的属性值和/或当前缩放级别，来生成适当的样式属性或过滤器。

适用于iOS的Mapbox地图SDK允许您使用 [`NSExpression`](https://developer.apple.com/documentation/foundation/nsexpression) 创建符合Mapbox样式定义的表达式。在本教程中，您将创建属性和缩放表达式来有条件地改变图层样式。

一个**数据表达式**是使用要素属性数据的表达式。属性表达式允许要素外观根据其属性改变。他们可以用于在同一图层中从视觉上区分不同的要素类型或者创建数据可视化。


{{
  <Note title='从早期的地图SDK版本迁移 (<4.0.0)' imageComponent={<BookImage />}>
    <p>如果您已经使用旧版本的适用于iOS的Mapbox地图SDK在运行时定义您数据的样式，请阅读我们的 <a href="https://www.mapbox.com/ios-sdk/api/{constants.VERSION_IOS_MAPS}/migrating-to-expressions.html">迁移指南</a> 来学习更多关于如何将样式函数转换为表达式的信息。</p>
  </Note>
}}

## 用途
有数不尽的方式来将属性表达式应用于您的程序，包括：

- **数据驱动样式**：根据一个或者多个数据属性来指定样式规则，例如根据人口数量来对洲多边形进行着色。
- **算术**: 对源数据进行计算，例如执行计算来动态转化单位。
- **条件逻辑**: 使用if-then逻辑，例如根据要素中可用的属性或者名称的长度来决定显示标签的文本。
- **字符串操作**: 接管标签文本的显示例如大写，小写，首字母大写，而无需编辑、重新准备和重新上传数据。


在本教程中，您将学习如何使用表达式来根据年龄和缩放级别来设置明尼阿波利斯市历史保护委员会地标的样式。

## 创建地图

### 初始化地图视图

在构建数据可视化之前，您需要先初始化地图视图。使用以下的代码来创建一个使用[Mapbox Light](https://www.mapbox.com/maps/light-dark/)样式的地图视图，然后以明尼苏达州明尼阿波利斯为中心：

{{
  <IosCodeToggle
    id='code-initialize-a-map-view'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[6,17]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[9,22]]}
  />
}}


结果将是如下所示的以Mapbox Light样式的空白地图：

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-simple-mapview.png' alt='blank light map on an iOS device' /></div>
</div>
}}

### 上传数据

在本指南中，您将使用[矢量tileset](/help/glossary/tileset) 来在您的程序中展示数据。您可以通过向Mapbox Studio上传之前您下载的CSV来创建一个矢量tilese：

1. 访问Mapbox Studio中的 [Tilesets 页面](https://www.mapbox.com/studio/tilesets) 页面。
1. 点击 **New tileset**.
1. 选择您在本教程开始下载的CSV文件然后点击 **确认**。
1. 右下方将出现一个弹窗显示您上传的进度
1. 上传 _成功_ 后，tileset就可以使用了。点击弹窗中tileset的名称，将打开tileset信息页面。
1. 记下tileset页面右侧的*tileset ID*，您将在下一步使用该ID来向您的地图中添加tileset。

### 将源数据添加到地图中

要将数据添加到地图中，您需要做以下两件事：

1. 将矢量tileset作为[`MGLVectorTileSource`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLVectorTileSource.html)动态地添加至地图以便在最初加载源数据。
2. 添加一个对应的`MGLCircleStyleLayer`来引用上边的`MGLVectorTileSource`以便在地图上展示数据。

源数据和图层样式应该在地图加载完成后添加，因此两者的代码都应该在委托方法{{<a href="https://www.mapbox.com/ios-sdk/api/{constants.VERSION_IOS_MAPS}/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:didFinishLoadingStyle:"><code className="highlighter-rouge">-mapView:didFinishLoadingStyle:</code></a>}}中。

{{
  <IosCodeToggle
    id='code-add-the-source-data-to-the-map'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[19,31],[40,41]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[25,37],[46,47]]}
  />
}}

当您运行您的程序的时候，您将看到tileset已经作为数据源添加至地图。您现在可以看到每个地标被指定颜色和透明度的圆圈标记。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-add-source.png' alt='adding a new circle layer to a map' /></div>
</div>
}}

### 使用表达式来计算每个地标的年龄

下一步，您将写表达式来根据每个历史地标的年龄来设置圆圈的半径。在这个明尼阿波利斯开源数据数据门户提供的数据文件中，没有提供历史地标的年龄，但是提供了建造年份。

您可以根据当前年份使用算式来计算每一个地标的年龄，而不是编辑源数据并重新上传。在计算了每个地标的年龄以后，您可以根据每个地标计算出来的年龄设置[`circleRadius`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLCircleStyleLayer.html#/c:objc(cs)MGLCircleStyleLayer(py)circleRadius)的绘制样式。

首先计算地标的年龄，并将其作为圆圈的半径，以便更久远的建筑的圆圈更大。

```swift
layer.circleRadius = NSExpression(format: "2018 - Constructi")
```

```objectivec
layer.circleRadius = [NSExpression expressionWithFormat:@"2018 - Constructi"]
```

以上的表达式用当前年份（2018）减去每个要素的建造时间。`Constructi`是每个地标对应的建造时间。再次运行程序来查看变化。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-calculate-age.png' alt='change the radius of each circle based on the age of each landmark' /></div>
</div>
}}

哇哦！这些圆圈太大了。这是因为半径用屏幕点来计算，而`Constructi`用年来计算。要让它变得更好看，您需要对圆的半径做一些调整。

### 调整圆的半径

既然表达式可以支持数学运算，您可以使用已有的表达式并将年龄除以10来减小每个圆圈的半径。

```swift
layer.circleRadius = NSExpression(format: "(2018 - Constructi) / 10")
```

```objectivec
layer.circleRadius = [NSExpression expressionWithFormat:@"(2018 - Constructi) / 10"]
```

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-reduce-circle-radius.png' alt='reduce the size of each circles radius' /></div>
</div>
}}

那看起来更好。减少圆的大小让地图在当前缩放级别下更易读的。在当前缩放级别仍有圆圈重叠，所以让我们添加一个缩放表达式来根据地图当前缩放级别调整圆的半径。

### 添加缩放表达式

在初始的10缩放级别，圆圈仍有大量重叠，但他们在更高的缩放级别看起来挺好。您可以使用缩放表达式来解决这个问题，它允许图层根据地图的缩放级别来调整样式。缩放表达式可以创造立体感效果和控制数据密度。

您将新建一个线性的插值表达式在以下的缩放级别定义不同的圆圈半径：

| 缩放级别 | 圆半径    |
|------------|------------------|
| 0-10       | 计算的建筑年龄 ÷ 30 |
| 13+        | 计算的建筑年龄 ÷ 10 |

通过使用线性插值，圆半径将在同一分类下保存一致。例如在18的缩放级别，圆的半径还是计算的建筑年龄除以10。还有其他的插值方法有不同的解释，您可以在[Maps SDK 文档](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Categories/NSExpression%28MGLAdditions%29.html#/c:objc(cs)NSExpression(cm)mgl_expressionForInterpolatingExpression:withCurveType:parameters:stops:)阅读更多详细内容。

在您的代码中，线性插值表达式如下所示：

{{
  <IosCodeToggle
    id='code-calculate-add-a-zoom-expression'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[33,39]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[39,44]]}
  />
}}

{{
  <Note imageComponent={<BookImage />}>
    <p>如果您以前使用过 <a href='https://www.mapbox.com/mapbox-gl-js/style-spec/#types-function'>属性 <em>函数</em></a>， 请注意<code>MGLInterpolationModeExponential</code>表达式允许您实现与在数据源停止时使用`MGLStyleValue`相同的效果。</p>
  </Note>
}}

当您再次运行程序的时候，您将看到在相同缩放级别，圆圈显示更清晰。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-post-zoom-expression.png' alt='adjust the circle radius based on zoom level' /></div>
</div>
}}

## 完成的产品

您已经使用适用于iOS的Mapbox地图SDK的表达式自定义数据样式！

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'>
    <video autoPlay loop width="100%" className="block" src='/help/img/ios/ios-dds-circle-layer-result.mp4' type='video/mp4'></video>
  </div>
</div>
}}

您可以在下边找到本教程完整的代码：

{{
  <IosCodeToggle
    id='code-finished-product'
    swiftCode={snippet.finalSwift}
    objectiveCCode={snippet.finalObjc}
  />
}}
