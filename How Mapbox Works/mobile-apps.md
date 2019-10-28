---
title: Mobile applications
description: Learn how the Mapbox mobile SDKs work and how to add Mapbox maps to a mobile application.
image: /img/narrative/mobile-develop.svg
topics:
  - mobile apps
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: guide
---

[Mapbox Maps SDK for iOS](https://docs.mapbox.com/ios/maps/overview) 和 [Mapbox Maps SDK for Android](https://docs.mapbox.com/android/maps/overview) 都是将Mapbox底图添加到移动应用的开源工具。这些SDK利用Mapbox基于OpenGL的开源渲染器 [Mapbox GL Native](https://github.com/mapbox/mapbox-gl-native)，并支持一整套的动态造型功能与交互。你可以不用退出应用来加载自定义的Mapbox样式、运用Mapbox Geocoding API来搜索定位、或者获取路线。如果可能，Mapbox Maps SDKs for iOS and Android会为一般平台专用的地图SDK提供嵌入的替代。

本指南会说明Mapbox mobile SDK如何工作以及如何将Mapbox服务加入移动应用。

<img src="/help/img/mobile/mobile-dds.jpg" alt="unity screenshot">

## Mapbox mobile SDKs 如何工作

The Mapbox Maps SDKs for [iOS](https://docs.mapbox.com/ios/maps/overview/) 和 [Android](https://docs.mapbox.com/android/maps/overview/) 允许你将交互地图添加到你的移动应用、定义自定义及动态样式规则、处理自定义数据、并与Mapbox网页API连接。

### 用户端渲染

Mapbox mobile SDK的核心是Mapbox GL：一个强大的渲染引擎，它可以阅读**raw data** 和 **style rules** 然后在设备上输出完整的渲染地图。由于传统的服务器端的渲染只能生成静态图块，而结果图块一旦到达用户则无法渲染。运用Mapbox GL，图块可以直接在用户端渲染。这样你可以创建动态可视化，且可以动态移除图层。

### 图层和运行时样式设置

许多受欢迎的地图函数库都遵守 "basemap-overlay" 的范式，即一张地图由两种独特类型的图层组成：底图（一张提供基础与上下文信息的完整地图）和覆盖图层（常是运行时加载在地图之上的交互数据）。

#### 图层

底图-叠加策略在长时间内效果都很好，但也有许多缺点。叠加图层常会压盖底图的标注且叠加的大数据集很快就会变得累赘。

Mapbox地图脱离底图-叠加策略并且将地图上的 _所有要素_ 都作为你可以独立设置样式与在渲染堆栈中上下移位的图层来处理。在这种显示地图的方法下，一个图层是一个 **styled representation of vector or raster data** ，它被以Mapbox的规则渲染。这个策略使得数据在被添加时不对上下文要素如注记产生压盖。

#### 运行时样式设置

因为地图上的所有内容都是在设备上从矢量或栅格图块实时渲染而来，所以Mapbox地图在地图与叠加图层上没有区别。这意味着 _every element of the map_ 都可以在运行时[runtime](/help/glossary/runtime-styling/) 被添加、移除及动态设置样式，与其他制图函数库中的叠加图层一样。

#### 数据驱动样式设计

[Data-driven styling](/help/glossary/data-driven-styling/) 使得你可以基于数据属性来改变地图样式。例如，你可以根据十字路口通行的行人数量来设置路口的半径，或者你也可以根据每个州的人口数量来更改各个州的填充色。

<div class='align-center'><img alt='graduated circle map using data-driven styling' src='/help/img/screenshots/dds-pedestrian_foot_traffic_at_intersections.png'></div>

### 要素查询与交互

在设备上进行运行时地图渲染的一个好处是，这样使得地图用户可以查询地图上的 _any feature_ ，包括曾被认为是“底图”的内容。使用 [feature querying](/help/glossary/feature-querying/)，你可以添加交互至你的任意地图样式中。比如，你可以使用要素查询来开发一个应用，使你的用户在点击一个公园多边形时能打开一个含有该公园信息的弹窗。

Mapbox mobile SDK 包括查询要素的方法，无论它们有没有被渲染，但只有在地图视野中加载的图块内的要素才能被查询。探索 [Select a feature using feature querying](https://docs.mapbox.com/ios/maps/examples/select-layer/) 示例来观看要素查询的过程。

<div class='align-center'><img alt='selecting individual states with feature querying' src='/help/img/mobile/mobile-select-layer.gif'></div>

### 照相机

照相机是地图的可视范围。很多常见地图函数库中照相机的视角取决于地图的中心点和缩放级别。移动SDK也包括一些调整地图视角的参数。

- **Centerpoint**: 按经度、纬度顺序，以小数表示度数。
- **Zoom level**: 任何0到22之间的数字。可以有小数部分，如1.5或6.2。
- **Bearing**: 以度数来表示的地图旋转情况。当正向旋转时，地图会旋转，文字注记也会相应变化。
- **Tilt**: 地图透视倾斜的数值，也以度数表示。

### 离线地图

使用我们的移动SDK开发的应用可以在设备无法联网的情况下下载选定区域的地图。如果有些应用的用户需要去到数据链接状况不太好的地区，或者他们想在出国时节省移动数据漫游费用，那么离线地图对这些应用是非常有用的。

如果想要估算离线下载区域所需要的图块数量，请使用我们的离线图块付算器。请注意，这样只能得到一个估算 _estimate_ 的数字，实际数据大小 _size_ 取决于需要下载的位置以及应用中使用的样式。

<a class="txt-ms txt-bold link" href="/help/interactive-tools/offline-estimator/">Offline tile count estimator{{<Icon name='arrow-right' inline={true} />}}</a>

我们的移动SDK也可以自动缓存应用正常使用时需要的图块和其他资源。这些资源和离线资源存储在同一个数据库，但与离线资源不同的是，这些资源限制在50MB的空间内。达到限制空间时，不被[offline region](/help/glossary/offline-region/)共享的、最久前使用的资源会被移除，以腾出空间给较新的资源。

更多关于如何在不同操作系统下使用离线地图的信息请分别参考[iOS](https://docs.mapbox.com/ios/api/maps/{{constants.VERSION_IOS_MAPS}}/Classes/MGLOfflineStorage.html) 和 [Android](https://docs.mapbox.com/android/maps/overview/offline/)。更多关于离线地图的背景知识，请阅读我们的[Offline maps](/help/troubleshooting/mobile-offline) 故障排除指南。

### Telemetry

默认设置下，当你的应用能收集到用户定位时，它会向Mapbox发送匿名定位与使用数据。但你的用户应该对他们的定位数据与何时分享负责。

如果你在使用Mapbox移动SDK开发一个本地应用，我们的服务条款要求你在app内向所有终端用户提供一个 [telemetry](https://www.mapbox.com/telemetry/) opt-out 选项。默认attribution control包括一个 opt out 按钮。如果你隐藏了[attribution control](/help/how-mapbox-works/attribution/)，那么你必须提供一个替代的opt out方式供你的用户使用。你有责任允许你的用户退出使用 （opt-out） Mapbox Telemetry。

## 添加Mapbox至你的移动应用

Mapbox提供了一系列工具来帮助你将Mapbox地图与我们其他的网络服务结合运用至你的移动应用，比如导航、地理编码、静态地图。

### 地图

首先，访问移动SDK概述页面，它包括安装说明，API文档，及一些示例代码：

- [Mapbox Maps SDK for Android](https://docs.mapbox.com/android/maps/overview/)
- [Mapbox Maps SDK for iOS](https://docs.mapbox.com/ios/maps/overview/)

如果你想要更明细的指南介绍来帮助开发你的第一个使用我们Maps SDKs的移动应用，请浏览我们的起步指南：

- [First steps with the Mapbox Maps SDK for iOS](/help/tutorials/first-steps-ios-sdk/)
- [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/)

### Mapbox 网络服务

为使 Mapbox Maps SDKs for iOS and Android 尽量精简，我们提供独立的函数库以连接Mapbox网络服务如[Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions), [Geocoding API](https://docs.mapbox.com/api/search/#geocoding), 和 [Static Images API](https://docs.mapbox.com/api/maps/#static-images)。

在Android上，**Mapbox Java SDK** 提供方便的接口以连接很多Mapbox网络服务API和小部分完成常用空间任务的实用工具。

在iOS上，**MapboxGeocoder.swift**, **MapboxDirections.swift**, 和 **MapboxStatic.swift** 提供接口以连接 Mapbox Geocoding API， Directions API, 和 Static Images API。

请访问各平台的相应文档页面以获得安装说明、API文档、示例代码：

- [Mapbox Java SDK](https://docs.mapbox.com/android/java/)
- [Mapbox API libraries for iOS](https://docs.mapbox.com/ios/maps/overview/#integration-with-other-tools)

### Mapbox Navigation SDKs

[Mapbox Navigation SDKs](/help/glossary/mapbox-navigation-sdk/) 建立在 [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) 的基础上，它提供所有必要逻辑以在你的应用中打造一个导航体验。Mapbox Navigation SDKs 包括关键功能如：

- 嵌入式路线规划UI
- 驾车、骑行与步行导航
- 避开拥堵
- 智能提醒
- 文字导航
- 文字转语音支持
- 路线自动切换
- 路径吸附

想要在你的应用中使用Mapbox Navigation SDKs，请访问相应的文档页面以获得安装说明、API参考及示例代码：

- [Mapbox Navigation SDK for iOS](https://docs.mapbox.com/ios/navigation/overview/)
- [Mapbox Navigation SDK for Android](https://docs.mapbox.com/android/navigation/overview/)

### 混合架构
第三方开发了允许你在多个替换开发平台上使用Mapbox SDKs的插件和集成。

请参见我们的[hybrid pricing guide](/help/account/pricing/#hybrid-applications) 以了解更多应用使用的资费信息。

#### 使用 Mapbox JavaScript APIs 的混合架构

用[Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js) 或[Mapbox.js](https://docs.mapbox.com/mapbox.js) 创建混合应用。

#### 潜在问题

如果你有想法或遇到问题，请直接联系各集成的管理员，因为我们没有办法就混合架构提供官方的支持。

[iOS](https://docs.mapbox.com/ios/maps/overview/) 和 [Android](https://docs.mapbox.com/android/maps/overview/) 平台上的Mapbox Maps SDKs 开发发展迅速，新功能定期发布。依托这些本地SDK的第三方插件可能与新版本不一致，滞后于官方发布版本，或无法支持所有可用功能。

<!--copyeditor disable best-->

我们的本地SDK在你直接使用时运行最优。现在就开始使用吧，请参见我们适用于 [Android](/help/tutorials/first-steps-android-sdk) 和 [iOS](/help/tutorials/first-steps-ios-sdk) 的新手指南。
