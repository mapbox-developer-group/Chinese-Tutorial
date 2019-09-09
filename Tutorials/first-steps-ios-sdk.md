---
title: 新手入门：开始使用Mapbox Maps SDK（iOS）
description: 学习如何安装Mapbox Maps SDK（iOS），在屏幕上显示地图，以及在地图上进行标记。
thumbnail: firstStepsiOS
level: 1
topics:
- mobile apps
language:
- Swift
- Objective-C
prereq: 熟悉Xcode和Swift（或Objective-C），并完成Mapbox Maps SDK（iOS）的安装教程。
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { IosCodeToggle } from '../../components/ios-code-toggle'"
  - "import * as snippet from '../../snippets/first-steps-ios-sdk.js'"
contentType: tutorial
---


[Mapbox Map SDK (iOS)](https://www.mapbox.com/ios-sdk) 是Mapbox面向iOS提供的矢量地图库。本节内容将展示如何使用Map SDK (iOS），具体内容包括如何制作自定义地图，如何添加地图标记和标注框，以及如何在地图上显示用户定位。


## 新手入门

首先，按照 [安装指南](https://www.mapbox.com/install/ios/) 安装面向iOS的Mapbox Maps SDK。您可以用依赖管理器（如Carthage或CocoaPods）或者手动安装SDK来完成Mapbox Maps SDK（iOS）的整合。

完成安装流程后，当您选择 **“Add with code”** 选项时，您的视图控制器（view controller）应该如下所示一样。如果您在安装过程中选择了 **“Add with Storyboard”** 选项，为了继续完成本节教程，您需要将 [`MGLMapView`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html) 连接到一个 `IBOutlet`，使得它在您的视图控制器内都是可使用的。

{{
  <IosCodeToggle
    id='code-getting-started'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[8,11]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[13,16]]}
  />
}}

### 改变地图样式

通过设置 [`MGLMapView.styleURL`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)styleURL) 的属性为一个[样式URL](/help/glossary/style-url) 来改变地图样式。这个样式URL可以是Mapbox提供的精美[模板](https://www.mapbox.com/maps/) 或者 [设计者样式](https://www.mapbox.com/designer-maps/)，您也可以在 [Mapbox Studio](https://www.mapbox.com/studio-manual/)创建完全自定义样式。

类[`MGLStyle`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLStyle.html)也提供了一系列返回 [Mapbox默认样式](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLStyle.html#/Accessing%20Default%20Styles)URL的函数。

在本教程中，您将使用Mapbox卫星街景图样式。将 [`MGLMapView.styleURL`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)styleURL) 的属性设置为 [`satelliteStreetsStyleURL`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLStyle.html#/c:objc(cs)MGLStyle(cm)satelliteStreetsStyleURL) 。

{{
  <IosCodeToggle
    id='code-change-the-map-style'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[13,13]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[18,18]]}
  />
}}

然后运行您的应用程序就可以看到设置的地图新样式。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-satellite-style.png" className='wmax300' alt="Satellite map on iOS app" /></div>
</div>
}}

## 添加地图标记

添加地图标记或者 [标注](/help/glossary/annotation/) 可以通过有多种方式来实现，其中`MGLPointAnnotation` 提供了最简单的方式在地图上添加预定义的点样式。

如下 `viewDidLoad` 函数中的代码显示了如何在纽约中央公园的位置上添加点标注。

{{
  <IosCodeToggle
    id='code-add-a-marker-to-the-map'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[15,20]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[20,25]]}
  />
}}

运行您的应用程序就可以看到新添加的点标注。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-add-marker.png" className='wmax300' alt="Map with marker on Central Park" /></div>
</div>
}}

`MGLPointAnnotation` 是所有点标注的基类，可以用视图或者静态图片对它进行设置，从而代替预定义的点标注样式。您可以阅读教程 [`MGLAnnotationView`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLAnnotationView.html) 和 [`MGLAnnotationImage`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLAnnotationImage.html)获取更多以上两种点标注样式的信息。  

如果您需要在地图上添加大量的点，可以考虑使用运行时样式化（runtime styling），这也是致力于实现大数据可视化的Mapbox Maps SDK （iOS）的一大特色。您可以阅读教程 [Markers and annotations](https://www.mapbox.com/ios-sdk/maps/overview/markers-and-annotations/) 了解在地图上添加点的不同方式以及它们之间的区别。

### 添加标注框

当用户点击地图标注时，为了显示一个标注框，您的视图控制器需要使用 [`MGLMapViewDelegate`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Protocols/MGLMapViewDelegate.html) 提供的符合 `MGLMapViewDelegate` 协议的委托函数（delegate methods）。

当视图控制器符合 `MGLMapViewDelegate` 协议并且地图视图的委托（delegate）被设置为视图控制器时，您就可以实现 <code><a href="https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:annotationCanShowCallout:">-mapView:annotationCanShowCallout:</a></code> 委托函数。这就实现了地图视图在被点击时自动显示标注框的功能。完整的实现方法如下：

{{
  <IosCodeToggle
    id='code-add-a-callout'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[22,23],[29,32]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[30,31],[34,37]]}
  />
}}

运行应用程序，然后点击地图标注––––点击后将出现一个带`标题`and`副标题`的标注框！

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-add-callout.png" className='wmax300' alt="satellite map on iOS app" /></div>
</div>
}}

### 局部放大至地图标记

当标记被点击时，设置地图的中心点为该标记处。为了实现这个功能，首先要实现 [`-mapView:didSelectAnnotation:`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:didSelectAnnotation:) 委托方法。 当委托函数被调用时，定义并初始化一个新的地图视野 &mdash; [`MGLMapCamera`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapCamera.html) 。然后就可以在 `MGLMapView` 上调用 [`-setCamera:animated:`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(im)setCamera:animated:) ，以此来设置新的地图视角。新的地图视角将以地图标记坐标处为中心，并可以设置地图视角离地面的距离。

{{
  <IosCodeToggle
    id='code-zoom-to-a-marker'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[34,38]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[39,43]]}
  />
}}

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-zoom-marker.gif" className='wmax300' alt="zooming to marker" /></div>
</div>
}}

## 显示用户位置

首先，为了使用设备定位服务，您需要设置用户定位许可。在您在地图上绘制用户位置前，您需要获得用户的定位许可并给出您将如何使用用户位置信息的简短解释。

通过设置Info.plist文件中的 `NSLocationWhenInUseUsageDescription` 可以设置定位许可。我们推荐将其值设置为： `Shows your location on the map and helps improve OpenStreetMap` 。此外，您还可以选择是否将 `NSLocationAlwaysAndWhenInUseUsageDescription` 放入Info.plist文件。我们推荐将其设置成为一个不同的值，方便用户决定他们给予应用的定位许可等级。当用户第一次打开应用时，他们将会收到一个提醒来询问他们是否允许该应用获得他们的位置信息。

{{
<注意 imageComponent={<BookImage />}>
  <p>如果您的应用是以iOS 10或者更低版本为目标的，您可能需要在您的应用中包含 `NSLocationAlwaysUsageDescription` 。注意这个密钥已经不在iOS 11中使用了。
  </p>
</Note>
}}

一旦您设定好应用的定位许可，您就可以通过设置地图视图中的 [`showsUserLocation`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)showsUserLocation) 的属性为 `true` 来显示设备的当前位置。

{{
  <IosCodeToggle
    id='code-display-the-users-location'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[25,27]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[27,29]]}
  />
}}

### 模拟定位

当您在Simulator中运行应用程序时，询问是否使用定位服务的对话框将会弹出。点击 **Allow** 。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-user-location-permission.png" className='wmax300' alt="Location permissions alert" /></div>
</div>
}}

您暂时将不会看到在地图傻姑娘看到您的定位。在Simulator的菜单中选择 **Debug ‣ Location ‣ Custom Location** ，在纬度处输入 `40.74699` ，在经度处输入 `-73.98742` ，然后您就可以看见您的定位在纽约中央公园外！

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-user-location.png" className='wmax300' alt="Map displaying user location" /></div>
</div>
}}

## 最后成品

{{
  <IosCodeToggle
    id='code-finished-product'
    swiftCode={snippet.finalSwift}
    objectiveCCode={snippet.finalObjc}
  />
}}

## 下一步

您成功使用了Mapbox Maps SDK（iOS）开发了一个小型应用程序！您学会了在iOS应用中添加Mapbox地图，改变地图样式，添加地图标注，在地图上显示用户定位。做得好！

为了您继续开发您的Mapbox应用，我们推荐您阅读以下教程：

* [Mapbox Maps SDK for iOS homepage](https://www.mapbox.com/ios-sdk) &mdash; 使用Mapbox Maps SDK（iOS）的基本信息。
* [Mapbox Maps SDK for iOS documentation](https://www.mapbox.com/ios-sdk) &mdash; 所有类和函数的完整参考。 
* [Mapbox Maps SDK for iOS code examples](https://www.mapbox.com/ios-sdk) &mdash; 类和函数的应用实例。 
* [Mapbox GL Native on GitHub](https://github.com/mapbox/mapbox-gl-native) &mdash; 使用Mapbox Maps SDK（iOS）的开源项目。
