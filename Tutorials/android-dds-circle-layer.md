---
title: 针对安卓的数据驱动样式
description: 创建一张安卓地图，并基于属性数据设计一个圆的样式。

thumbnail: androidDdsCircleLayer
level: 2
topics:
- mobile apps
language:
- Java
前提: 您已创建好一个包含地图视图的安卓应用程序，并且熟悉 Android Studio 和 Java。
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-dds-circle-layer.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

[数据驱动样式](/help/glossary/data-driven-styling/) 是 Mapbox Maps SDK for Android 的一个强大特性，其允许您使用属性数据来设计地图样式。通过数据驱动样式，您可以全自动地定义基于各属性的地图要素样式。 在本教程中，您将创建一张依据属性数据设计样式，包含圆形图层的Android地图。

<div class='align-center'>
<img src='/help/img/android/android-dds-style-by-attribute.png' alt='map with data styled by attribute on an Android device' class='inline wmax360-mm wmax-full'>
</div>

## 开始

本教程假定您已经熟悉 Java 和 Android Studio。以下是您开始前需要的一些资料：

- **一个包含 Mapbox Maps SDK for Android 的应用程序。** 本教程假定您已创建了一个基于 Mapbox Maps SDK for Android 的安卓应用程序。如果 Maps SDK for Android 对您来说还是陌生的，请先参考教程 [Mapbox Maps SDK for Android 起步](/help/tutorials/first-steps-android-sdk/) 来创建一个地图视图。
- **数据。** 我们从哥伦比亚特区的 [Open Data DC](http://opendata.dc.gov/) 收集了其行道树的位置数据。每一棵树都有一个 `DBH` 属性，代表 [树胸高直径](https://en.wikipedia.org/wiki/Diameter_at_breast_height)，用来衡量树的大小。

{{
<Button href="/help/data/street-trees-DC.zip" passthroughProps={{ download: "street-trees-DC" }} >
    <Icon name='arrow-down' inline={true} /> Download Shapefile
</Button>
}}

## 上传数据到 Mapbox

在本教程中，您将使用 [向量瓦片集](/help/glossary/tileset) 来在您的应用中展示数据。您可以通过上传 Open Data DC 的 Shapefile 到 Mapbox Studio 来创建向量瓦片集：

1. 登录 [Mapbox Studio](https://www.mapbox.com/studio)。
1. 访问 [瓦片集页面](https://www.mapbox.com/studio/tilesets)。
1. 点击 **新瓦片集**。
1. 选择您之前下载好的 Shapefile 并点击 **确认**。
1. 右下角将出现一个弹出框，显示上传进度。
1. 一旦上传 _完成_, 瓦片集即可使用！点击弹出框里的瓦片集名称，会打开该瓦片集的详情页面。
1. 请记录该详情页面右侧的 **Tileset ID**。稍后，您将使用该ID来添加此瓦片集到您的应用程序。

## 初始化一个地图视图

在 Android Studio 中创建一个新项目并初始化一个地图视图。为使用 Android Studio 项目创建一个 Mapbox 地图，并添加定制化数据来使用数据驱动样式，您需要以下5个文件：

- **build.gradle**: Android Studio 使用 Gradle 工具集将源文件和源代码编译成一个 APK 文件。`build.gradle` 文件被用来配置构建和管理包括Mapbox Maps SDK for Android 在内的依赖。
- **AndroidManifest.xml**: 您可以在 `AndroidManifest.xml` 文件中描述应用程序的组件，比如与 Mapbox 相关的权限。
- **activity_main.xml**: 您可以在 `activity_main.xml` 文件中设置地图视图的属性（例如地图视图的中心, 缩放级别以及地图样式）。
- **strings.xml**: 您可以将 access token 存储在 `strings.xml` 文件中。
- **MainActivity.java**: 您可以在 `MainActivity.java` 文件中指定 Mapbox 的各种交互。

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>build.gradle (App module)</div>
}}

```groovy
// in addition to the rest of your build.gradle contents
// you should include the following repository and dependency
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.mapbox.mapboxsdk:mapbox-android-sdk:{{constants.VERSION_ANDROID_MAPS}}'
}
```

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>Manifest.xml</div>
}}

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```



{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
  />
}}

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>strings.xml</div>
}}

```xml
<string name="access_token" translatable="false">{{ <UserAccessToken /> }}</string>
```

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,10],
      [23,40],
      [63,67],
      [70,111]
    ]}
  />
}}

您可以在 [Mapbox Maps SDK for Android 起步](/help/tutorials/first-steps-android-sdk/) 教程中学习如何在 Android Studio 创建一个包含 Maps SDK for Android 的项目。

运行您的应用程序，您将会看到一张中心位于 Logan Circle 的 Mapbox Dark 样式地图。

<div class='align-center'>
<img src='/help/img/android/android-dds-initialize-map.png' alt='initialized map on an Android device' class='wmax360'>
</div>

## 载入资源

接下来，您需使用 [tileset ID](/help/glossary/tileset-id) 将之前添加到 Mapbox Studio 账户的瓦片集载入到应用程序中。您可以在 
[Mapbox Studio 中的瓦片集页面](https://www.mapbox.com/studio/tilesets/) 通过点击您上传的瓦片集旁的{{<Icon name='menu' inline={true} />}}图标来找到该 tileset ID。

首先，您需要在 `MainActivity.java` 文件中导入正确的类，这将允许您添加向量源并从数据创建一个圆形图层。

然后，添加代码来从瓦片集拉取数据，并将其创建成地图的一个图层。在 `MainActivity.java` 文件的 `public void onStyleLoaded(@NonNull Style style) { ... }` 里，添加如下代码：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [12,13],
      [41,50],
      [62,62]
    ]}
  />
}}

重新运行该应用程序，您将看到瓦片集的数据已经显示在黑色地图上了。值得注意的是，您将很难看到叠加在黑色底图上的黑色圆形。接下来，您需要设计数据的显示样式以使其更容易被看到。

<div class='align-center'>
<img src='/help/img/android/android-dds-load-data.png' alt='map with data on an Android device' class='wmax360'>
</div>

## 样式化图层

现在，您将改变每个圆形的颜色及其不透明度，以使数据更容易在黑色的底图上被看到。其次，您还需要基于 `DBH` 属性的值来设置每个圆形的大小。

### 改变颜色和不透明度

首先在 `MainActivity.java` 文件中导入正确的类。您将需要 `circleColor`， `circleOpacity` 这两个类。

然后，将如下代码添加到 `public void onStyleLoaded(@NonNull Style style) {...}` 方法里来指定图层的颜色和不透明度：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [15,16],
      [51,53],
      [61,61]
    ]}
  />
}}

重新运行该应用程序，您将在地图上看到同样的数据，但已变为白色并且半透明。

<div class='align-center'>
<img src='/help/img/android/android-dds-color-opacity.png' alt='initialized map on an Android device' class='wmax360'>
</div>


### 指定基于属性值的半径

最后，您将基于 `DBH` 值来指定圆形的半径。同样，您需要`Function` 以及 `exponential` 类来创建一个 property function， `Stop` 类来决定基于 `DBH` 值的圆形半径，`circleRadius` 类来设定 circleRadius paint property。

接下来，使用如下 exponential property function 替换`circleLayer.withProperties( ... )`中用来指定图层 paint properties 的代码：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [17,21],
      [54,60]
    ]}
  />
}}

重新运行该应用程序，您将看到数据样式已改变，每个圆形的半径取决于该数据点的 `DBH` 值。

<div class='align-center'>
<img src='/help/img/android/android-dds-style-by-attribute.png' alt='map with data styled by attribute on an Android device' class='inline wmax360'>
</div>

## 完结

您刚刚创建了一个数据可视化产品，用来展示华盛顿特区所有行道树的地理位置及其大小。

<div class='align-center'>
<img src='/help/img/android/android-dds-final-product.gif' alt='map with data styled by attribute on an Android device' class='inline wmax360'>
</div>

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## 下一步

使用数据驱动样式，您可以为您的安卓应用程序创建许多美丽、丰富的数据可视化效果。了解更多有关数据驱动样式，请参考 [Map design](/help/how-mapbox-works/map-design/)，更多基于安卓的数据驱动样式案例，请参考：

- [明确地定义圆形样式](https://github.com/mapbox/mapbox-android-demo/blob/master/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/dds/StyleCirclesCategoricallyActivity.java): 基于数据属性改变圆形图层里圆的颜色。
- [通过缩放级别更新](https://github.com/mapbox/mapbox-android-demo/blob/master/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/dds/ChoroplethZoomChangeActivity.java): 基于缩放级别显示州或者郡县的人口。
