---
title: 基于安卓设备的位置跟踪
description: 在安卓设备上显示一幅 Mapbox 地图，并实时更新当前位置
thumbnail: androidLocationTracking
level: 2
topics:
- mobile apps
language:
- Java
prereq: 熟悉 Android Studio 和 Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-location-tracking.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

[Mapbox Core Libraries for Android](https://docs.mapbox.com/android/core/overview/) 负责处理安卓项目中的系统权限、设备位置以及网络连接等事宜，例如:

- 检测、请求以及响应安卓系统的位置权限。
- 检测并响应设备的网络连通状态变化。
- 获取设备实时位置信息。

本教程将指导您添加 Mapbox 地图到安卓应用程序，并设置 Mapbox Core Libraries for Android 来获取设备的实时位置变化更新。您还将利用 Mapbox Maps SDK for Android 的 `LocationComponent` 组件来显示设备位置的图标。此外，位置变化更新信息包含了设备的实时地理位置坐标，可能对您的项目有所帮助。

本教程结束后，您的应用程序将显示一个 [Android system toast](https://developer.android.com/guide/topics/ui/notifiers/toasts)，每当 Core library 传递位置更新时，它都可以显示设备的最新位置坐标。除了利用 toast 显示位置坐标，您还可以选择您喜欢的其他方式：

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-final.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>


## 开始

首先在 Android Studio 中创建一个新项目并初始化一个地图视图。为了使用 Android Studio 项目创建一个 Mapbox 地图，并添加定制化数据来使用数据驱动样式，您需要以下5个文件：

- **build.gradle**: Android Studio 使用 Gradle 工具集将源文件和源代码编译成一个 APK 文件。build.gradle 文件被用来配置构建和管理包括 Mapbox Maps SDK for Android 在内的依赖。
- **AndroidManifest.xml**: 您可以在 `AndroidManifest.xml` 文件中描述应用程序的组件，比如与 Mapbox 相关的权限。
- **activity_main.xml**: 您可以在 `activity_main.xml` 文件中设置 `MapView` 的属性(例如 MapView 的中心, 缩放级别以及地图样式)。
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
      [1,13],
      [31,38],
      [48,71],
      [73,75],
      [203,235],
      [240,247]
    ]}
  />
}}

您可以在教程 [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) 中学习如何在 Android Studio 创建一个包含 Maps SDK for Android 的项目.

运行您的应用程序，您将看到一幅以美国田纳西州纳什维尔市为中心的 Mapbox Traffic Night 样式地图。

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-nashville-only.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>



## 处理位置权限

应用程序需要被安卓系统批准以使用设备位置追踪服务。Mapbox Core Library 负责位置权限的检查、请求以及相关响应。

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-permission-dialog.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>

通过使用 static check 返回的布尔值，您可以检测位置权限请求是否已经发送。如需创建一个位置权限请求，首先需要实现 `PermissionsListener` 接口。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [14,17],
      [39,40],
      [77,81],
      [111,111]
    ]}
  />
}}

实现 `PermissionsListener` 接口后，您需要重写 `onExplanationNeeded()` 方法。

向文件 `strings.xml` 添加一个名为 `user_location_permission_explanation` 的字符串资源，这样，当您需要在位置权限请求中提供更多说明信息时，该字符串将会显示。

```xml
<string name="user_location_permission_explanation">EXPLANATION_HERE</string>
```

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [128,136]
    ]}
  />
}}


方法 `onPermissionResult()` 也需要重写，其返回的布尔值表示用户接受或拒绝了应用程序的位置权限获取请求。获取位置权限后，则需初始化 Maps SDK 的 `LocationComponent` 组件。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [138,141],
      [143,148]
    ]}
  />
}}

创建一个新 `PermissionManager` 对象并调用其方法 `requestLocationPermissions()` 来检测权限。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [82,83],
      [107,110]
    ]}
  />
}}


## 初始化 `LocationEngine`

现在位置权限已经处理好了，我们需要创建一个 `LocationEngine` 对象。

首先创建一个 `LocationEngineRequest`。在请求中，定义如下：

- 位置更新的间隔（毫秒）。
- 位置更新的精度。
- 位置更新的最长等待时间（毫秒）。 在更新间隔测定位置，并根据等待时间的长短分批传递返回，但只有部分引擎支持分批这一特性。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [18,24],
      [41,44],
      [113,126]
    ]}
  />
}}

您可能还需添加如下代码到 `onDestroy()` 方法来防止内存泄漏：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [236,240]
    ]}
  />
}}


## 启用 `LocationComponent` 组件

{{<Note imageComponent={<BookImage />}>}}
本节是可选内容。如您无意在地图上显示位置图标，可跳过本节。
{{</Note>}}

通过 `PermissionsManager.areLocationPermissionsGranted(this)` 的布尔检查， 您已知晓应用程序已经获取了位置权限，同时 `LocationEngine` 也已经初始化。现在您可以安心地初始化 [Maps SDK 的 `LocationComponent` 组件](https://docs.mapbox.com/android/maps/overview/location-component/)。该组件可在地图上显示设备位置图标，但您**并非必须**显示该图标，因为其并不影响您继续阅读本教程。_因此，如您无意在地图上显示位置图标，可跳过本节_。

当 `LocationComponent` 组件的 `RenderMode` 选项是 `COMPASS` 时，位置图标的外部将显示一个箭头表征罗盘方位。该箭头指向设备的朝向。[有关其他 `RenderMode` 选项，请参考本链接](https://docs.mapbox.com/android/maps/overview/location-component/#rendermode)。

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-compass-arrow.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>

当`LocationComponent` 的 `CameraMode` 选项是 `TRACKING` 时，地图视野将随设备位置的变化而变化。[有关其他 `CameraMode` 选项，请参考本链接](https://docs.mapbox.com/android/maps/overview/location-component/#cameramode)。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [25,29],
      [72,72],
      [85,106],
      [142,142]
    ]}
  />
}}

## 监听位置变化

最后，我们将创建一个位置更新的接口回调来监听来自于 Mapbox Core Libraries for Android 的位置更新。

创建一个实现 `LocationEngineCallback<LocationEngineResult>` 接口的类，该接口是 Core Libraries 的一部分，同时请确保安卓系统的 `Activity` 作为该类的一个构造参数。值得注意的是，Activity/Fragment直接实现 `LocationEngineCallback<LocationEngineResult>` 接口可能引起 `LocationEngine` 内存泄漏，而创建此新类并设置 `WeakReference` 可避免该泄漏。

实现 `LocationEngineCallback<LocationEngineResult>` 接口需要重写 `onSuccess()` 和  `onFailure()` 方法。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [45,46],
      [150,201]
    ]}
  />
}}

每当 Mapbox Core Libraries 发现设备位置变化时，就会调用 `OnSuccess()` 方法。其中，`result.getLastLocation()` 方法返回一个包含经、纬度值的 `Location` 对象。现在，您可以通过您喜欢的方式使用该设备位置信息了，例如显示在应用程序的 UI 里 ，保存于内存中，或者发送到后端服务器。


## 完结

至此，您已配置好用来获得设备位置更新的代码。下方截图显示位于纳什维尔市，但实际上，如果 `LocationComponent` 组件的 `CameraMode` 选项仍是 `TRACKING`，地图视野将移动到任何您设备所在的位置。

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-final.gif' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## 下一步

`LocationComponent` 组件提供了很多可能性。 请参考 [Android 演示应用程序中的位置相关案例](https://github.com/mapbox/mapbox-android-demo/blob/master/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/location/)， 了解如何在 Android Fragment 中显示设备位置，定制 `LocationComponent` 组件图标等等。
