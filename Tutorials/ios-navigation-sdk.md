---
title: 创建一个iOS的导航程序
description: 可集成至任意的iOS程序。
thumbnail: iosNavigationSdk
level: 3
topics:
- mobile apps
- directions
language:
- Swift
- Objective-C
prereq: Familiarity with Xcode, Swift or Objective-C, and CocoaPods or Carthage.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { IosCodeToggle } from '../../components/ios-code-toggle'"
  - "import * as snippet from '../../snippets/ios-navigation-sdk.js'"
contentType: tutorial
---

适用于iOS的Mapbox导航SDK为您提供了向iOS程序添加逐向导航所需的所有工具。您可以在几分钟内启动并运行我们即插即用的导航视图控制器，或者使用我们的路由和导航的核心组件来构建一个完全自定义的程序。在这篇指南中，您将创建一个最小的导航程序，通过选择地图上的一个点开始导航，并更改导航视图控制器的样式。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img alt='an animated GIF of a navigation iOS app with turn-by-turn instruction' src='/help/img/ios/nav-sdk-full-nav.gif' className='hmax360' /></div>
</div>
}}

## 入门

[适用于iOS的Mapbox导航SDK](https://docs.mapbox.com/ios/navigation/) 可以在iOS 9.0及以上的版本上使用。它可以和Swift 4 及以上版本或者Objective-C 编写的代码一起使用。下面是您需要在开始之前需要的资源：

- **一个Mapbox账户和一个access token**. 在 [mapbox.com/signup](https://www.mapbox.com/signup/)上注册账户。 您可以在[Account page](https://www.mapbox.com/account/)页面找到您的[access tokens](/help/how-mapbox-works/access-tokens)。 您可以按照[installation instructions](https://www.mapbox.com/install/ios/)页面上的说明将access token添加至Info.plist文件。
- **一个包含适用于iOS的Mapbox地图SDK的程序。** 本指南假设您已经开始使用适用于iOS的Mapbox地图SDK来创建程序。如果您是新的适用于iOS的Mapbox地图SDK用户，请先完成 [First steps with the Mapbox Maps SDK for iOS](/help/tutorials/first-steps-ios-sdk/) 指南来创建一个地图视图。

## 安装适用于iOS的导航SDK

您可以使用CocoaPods 或者 Carthage 来安装适用于iOS的Mapbox导航SDK。 如果你是CocoaPods 或者 Carthage的新手，您可以从[CocoaPods](https://guides.cocoapods.org/using/getting-started.html) 和 [Carthage](https://github.com/Carthage/Carthage/#adding-frameworks-to-an-application)的文档开始。

###  安装框架

您需要将`MapboxNavigation`添加到您的构建中才能使用Mapbox导航SDK，地图服务和导向服务。

Cocoa pods:

```
pod 'MapboxNavigation', '~> {{constants.VERSION_IOS_NAV}}'
```

Carthage:

```
github "mapbox/mapbox-navigation-ios" ~> {{constants.VERSION_IOS_NAV}}
```


### 导入框架

在您将SDK导入构建中之后，您还需要将以下模块导入到您的`ViewController`中以便在程序中访问到它们。

{{
  <IosCodeToggle
    id='import-the-framework-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [1,4]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [1,5]
    ]}
  />
}}

## 初始化地图

在按照上一步将这些类导入后，您可以初始化一个地图。使用`NavigationMapView`来显示一个Mapbox默认样式的街道地图。`NavigationMapView`是`MGLMapView`的子类， `MGLMapView`提供了对导航程序特别有用的额外功能(例如在地图上显示路径)。`directionsRoute`变量稍后将用于引用由Mapbox导航SDK生成的路由。将以下的代码添加到视图控制器中。

{{
  <IosCodeToggle
    id='initialize-a-map-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [6,18],
      [27,27],
      [104,104]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [7,23],
      [32,32],
      [127,127]
    ]}
  />
}}


运行您的程序，您将看到一个新的地图。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img alt='a map in an iOS application' src='/help/img/ios/nav-sdk-initialize-map.jpeg' className='hmax360' /></div>
</div>
}}

{{
    <Note
      title='More resources'
      imageComponent={<BookImage />}
    >
        <p>您还可以使用适用于iOS的Mapbox地图SDK 执行更多的操作。 要了解更多可能的操作, 探索 <a href='/help/tutorials/first-steps-ios-sdk/'>First steps with the Mapbox Maps SDK for iOS</a> 和 <a href='/help/tutorials/ios-dds-circle-layer'>Data-driven styling for iOS</a> 教程。</p>
    </Note>
}}

### 展示用户位置

对应这个项目，您将获取用户位置和用户放置在地图上的点之间的规划路线。为此，您需要在您的程序中配置位置权限来获取设备位置。在您可以将用户位置绘制在地图上之前，您需要先征得用户的许可，并简要说明您的程序将如何使用他们的位置数据。

通过在Info.plist文件中设置 `NSLocationAlwaysUsageDescription` 或者 `NSLocationWhenInUseUsageDescription` 键来配置位置权限。我们建议将值设置为以下的字符串：`在地图上显示您的位置以及帮助优化OpenStreetMap`，作为程序位置信息的使用说明。当用户首次打开您的程序时，他们将会看到这个提示询问他们是否同意您的程序访问其位置信息。

{{
  <Note imageComponent={<BookImage />}>
    <p>在iOS 11 中，如果需要访问用户位置， 您 <strong>必须</strong> 在Info.plist文件中包含 <code>NSLocationWhenInUseUsageDescription</code> 键. 更多在iOS 11中追踪位置的信息， 我们建议您观看苹果的 <a href="https://developer.apple.com/videos/play/wwdc2017/713/">"What's New in Location Technologies"</a> 视频。</p>
  </Note>
}}

在您配置了程序的位置权限后，通过将`viewDidLoad`方法中的[`showsUserLocation`](https://docs.mapbox.com/ios/api/maps/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)showsUserLocation) 属性设置成`true`来将用户位置显示在地图上，并将[`MGLUserTrackingMode`](https://docs.mapbox.com/ios/api/maps/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)userTrackingMode) 设置成`follow`以便地图视窗跟随用户位置的更改更改。更新您视图控制器中`viewDidLoad`方法中的代码，以便显示用户位置以及开启追踪模式。

{{
  <IosCodeToggle
    id='display-user-location-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [20,22]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [25,27]
    ]}
  />
}}

当您在Simulator或者手机上运行程序您的程序时，您将看到一个对话框请求使用位置服务的权限。点击**允许**。在您打开Simulator的菜单栏，选择**调试 ‣ 位置 ‣ 自定义位置**，然后输入纬度`38.909`，经度`-77.036`之前，您无法在地图上看见您的位置。

{{
<div className='my12 clearfix align-center'>
  <div className='device contain device-phone-v'><img alt="a map displaying a user's location on an iOS device" src='/help/img/ios/nav-sdk-show-user-location.gif' className='hmax360' /></div>
</div>
}}

### 添加一个目的地

在这个程序中，您将假设用户想要检索一条在他们当前位置与他们在地图上选择的任意一点之间的规划路线。下一步，您将创建当用户点击并按住地图（[长按](https://developer.apple.com/documentation/uikit/uilongpressgesturerecognizer)）时，向地图添加一个标记或者[标注](/help/glossary/annotation/)的功能。这个目的地将计算导航路径时使用。

#### 创建一个手势识别器

首先创建一个名为`didLongPress`的方法。在这个方法中，获取用户所选的点并将其保存至名为`point`的变量中。然后，将点转换为地理坐标并将其保存在名为`coordinate`的变量中。在您定义的地理坐标新建一个[`MGLPointAnnotation`](https://docs.mapbox.com/ios/api/maps/{{constants.VERSION_IOS_MAPS}}/Classes/MGLPointAnnotation.html)并设置标题。标题稍后将在标注被选中时在气泡框中显示。在标注配置好后，将其添加至地图。如下所示，在您的视图控制器添加新的`didLongPress`方法。

{{
  <IosCodeToggle
    id='create-a-gesture-recognizer-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [29,40],
      [48,48]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [35,47],
      [57,57]
    ]}
  />
}}


稍后，您将添加另外一个方法来计算您原点到目的地之间的规划路线。

更新`viewDidLoad`方法，向您的`NavigationMapView`添加`UILongPressGestureRecognizer`，以便其接受新建的手势识别器。

{{
  <IosCodeToggle
    id='change-viewdidload-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [24,26]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [29,31]
    ]}
  />
}}

当您再次运行程序的时候，您将看到以用户位置为中心的地图。但这一次，如果您点击并按住地图上的任意一点，一个新的标记将放置在用户指定的位置。这个点标记了这个规划路径的目的地。下一步，您将创建一个计算规划路径本身的方法。

## 生成一个规划路径

要生成一个规划路径，您需要新建一个`Route`对象。当您安装Navigation SDK时，它也包含了`MapboxDirections.swift`。这提供了一种在iOS程序中访问[Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions)的便捷方式，并用于生成在Navigation SDK 中用于展示逐向方向的`Route`对象。

Mapbox Directions API 需要至少两个航点来生成规划路线。您可以最多使用25个航点。更多有关航点的信息在[MapboxDirections.swift documentation](https://docs.mapbox.com/ios/api/directions/{{constants.VERSION_DIRECTIONS_SWIFT}}/Classes/Waypoint.html)。

在这个项目中，您将使用两个航点 **原点** 和 **目的地**。对于这种情况，原点是用户的位置，目的地是用户放置在地图上指定的点。对于每个航点，您将使用`Waypoint`类来指定纬度、经度以及用于描述位置的名称。

通过创建包含以下代码的`calculateRoute`新方法，开始创建一个完整的导航体验：

{{
  <IosCodeToggle
    id='generate-a-route-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [50,65],
      [67,68]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [59,85],
      [87,88]
    ]}
  />
}}

#### 规划路径选项

在创建完新建您规划路径的方法后，使用`NavigationRouteOptions`类来设置一些选项来生成一条从原点到目的地的规划路径。这个类是MapboxDirections.swift中`RouteOptions`类的子类。您可以指定任意与 MapboxDirections.swift 中`RouteOptions` 类中可以使用的相同选项，但是默认选项更适合Navigation SDK如何使用规划路径的结果。在本例中，您将使用包含了高分辨率的规划路径和逐向导航指令步骤的默认选项。

{{
    <Note title='NavigationRouteOptions' imageComponent={<BookImage />}>
        <p>Read about all available <code>NavigationRouteOptions</code> in the <a href={https://docs.mapbox.com/ios/api/navigation/{constants.VERSION_IOS_NAV}/Classes/NavigationRouteOptions.html}>适用于iOS的导航SDK documentation</a>.</p>
    </Note>
}}

## 在地图上绘制规划路径

现在您您已经创建了一个计算规划路径的方法，创建另一个方法来在地图上 _绘制_ 规划路径。 创建一个变量引用您在入口视图控制器类中的规划路径对象，然后创建一个接收`Route` 对象作为参数的方法。使用输入的`Route` 对象的地理坐标来新建一个`MGLPolylineFeature`。在创建`MGLPolylineFeature`之后，将其添加至相应的样式图层中，同时配置各种样式属性，例如颜色和线宽。在您的视图控制器中创建一个名为`drawRoute`的新方法，



{{
    <Note imageComponent={<BookImage />}>
        <p><code>MGLPolylineFeature</code> 是许多可以添加至地图上的基础图形对象之一。在 <a href={https://docs.mapbox.com/ios/api/maps/{constants.VERSION_IOS_MAPS}/Primitive%20Shapes.html#/Primitive%20Shapes}>Maps SDK for iOS 文档</a>阅读更多有关向地图添加图形的信息。</p>
    </Note>
}}

现在，允许您的用户查看他们所选目的地的规划路径，更改`calculateRoute`方法来调用其中的 `drawRoute`方法。

{{
  <IosCodeToggle
    id='drawing-the-route-on-the-map-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [66,66],
      [70,91]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [86,86],
      [90,114]
    ]}
  />
}}

更新 `didLongPress` 方法以便在其中调用 `calculateRoute`方法。这将允许用户在地图上触发长按手势时规计算和绘制划路径。

{{
  <IosCodeToggle
    id='call-calculate-route-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [42,47]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [49,56]
    ]}
  />
}}

运行您的程序，并在地图上长按以选取目的地。当标记添加至地图后，将计算并绘制规划路径。

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img alt='drawing a navigation route in an iOS app' src='/help/img/ios/nav-sdk-draw-route.gif' className='hmax360' /></div>
</div>
}}

## 开始导航

要开始逐向导航序列，通过实现`annotationCanShowCallout`和`tapOnCalloutFor`这两个委托方法，允许标记显示一个气泡框并允许气泡框被选中。当气泡框被点击时，使用生成的规划路径来显示一个新的`NavigationViewController`。将这两个新方法添加至您的视窗控制器。

{{
  <IosCodeToggle
    id='start-navigating-code'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[
      [93,102]
    ]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[
      [116,125]
    ]}
  />
}}


## 完成的产品

允许程序然后选择并按住地图来添加标注。选中标注来显示一个气泡框，然后选中气泡框来初始化一个原点与您目的地之间的导航序列。您使用适用于iOS的Mapbox导航SDK构建了一个小的导航程序。您可以在GitHub上找到[指南的完整代码](https://github.com/mapbox/navigation-ios-examples/blob/master/DocsCode/NavigationTutorial/)

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img alt='an animated GIF of a navigation iOS app with turn-by-turn instruction' src='/help/img/ios/nav-sdk-full-nav.gif' className='hmax360' /></div>
</div>
}}

{{
  <IosCodeToggle
    id='finished-product-code'
    swiftCode={snippet.finalSwift}
    objectiveCCode={snippet.finalObjc}
  />
}}

## 下一步

除了您已完成的本教程外，还有许多您可以自定义 适用于iOS的Mapbox导航SDK 的方法。有关自定义选项的完整参考，请参阅[适用于iOS的导航SDK 文档](https://docs.mapbox.com/ios/api/navigation/{{constants.VERSION_IOS_NAV}}/)。选项包括：

- [行走和骑行模式](https://docs.mapbox.com/ios/api/directions/{{constants.VERSION_DIRECTIONS_SWIFT}}/Classes/RouteOptions.html#/s:vC16MapboxDirections12RouteOptions17profileIdentifierVSC29MBDirectionsProfileIdentifier)。
- [使用第三方语音合成器实现语音指令](https://docs.mapbox.com/ios/navigation/examples/custom-voice-controller/)。
- 使用[Core Navigation](https://github.com/mapbox/mapbox-navigation-ios/blob/v{{constants.VERSION_IOS_NAV}}/custom-navigation.md)创建一个自定义导航。
