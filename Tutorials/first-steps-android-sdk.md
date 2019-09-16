---
title: 新手入门：开始使用Mapbox Maps SDK（Android）
description: 学习如何安装Mapbox Maps SDK（Android），在屏幕上显示地图，以及在改变地图样式。
thumbnail: firstStepsAndroid
level: 1
topics:
- mobile apps
language:
- Java
prereq: 完成Mapbox Maps SDK（Android）的安装教程，熟悉Android Studio和Java。
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/first-steps-android-sdk.js'"
contentType: tutorial
---

Mapbox Map SDK (Android) 是Mapbox面向Android提供的矢量地图库。本节内容将教您如何安装Mapbox Map SDK (Android)的全过程，加载地图，改变地图样式，以及在地图上添加标记。

<div class='align-center'>
<img src='/help/img/android/android-first-steps-intro.png' alt='map with marker on an Android device' class='inline wmax360' />
</div>

## 新手入门

Here's what you'll need to get started:
开始之前，需要完成以下几个步骤：

- **Mapbox账户和access token**. 在 [mapbox.com/signup](https://www.mapbox.com/signup/) 注册一个Mapbox账户，您可以在您的 [用户页面](https://www.mapbox.com/account/) 找到您的access token。
- **Android Studio**. 您可以通过谷歌 [Android Studio](http://developer.android.com/sdk/index.html) 免费下载Android Studio。在开始安装Mapbox Map SDK (Android)之前，您需要下载Android Studio并创建一个空的工程。
- **一台Android设备（实体或者模拟器）**. 您需要一台实体Android设备或者一台 [模拟Android设备](https://developer.android.com/studio/run/emulator.html) 来预览商店探测器。
to preview the store finder.
- **Google Play开发者账户（可选）**. 如果您需要发布您的应用程序到Google Play，您将会需要一个 [Google Play开发者账户](https://play.google.com/apps/publish/signup/). 如果没有这个账户，您依然可以在Android模拟设备中预览您的应用程序或者在实体设备中安装它。

### 创建Android Studio工程

首先，请您熟悉Android Studio。您需要创建一个新的工程和一个空的activity，创建新工程时选择以下选项：

- 在选项 *Select the form factors your app will run on* 下, 选择"Phone and Tablet."
- 对于最低SDK版本， `select API 14: Android 4.0.0 (IceCreamSandwich)` 。(这是Mapbox Maps SDK （Android）能够支持的最低API版本）
- 点击 **Next** 跳转到activity选项页面.
- 选择 **Empty Activity** 并点击 **Next**.
- 直接选择默认的 `Activity Name` 和 `Layout Name` 并点击 **Finish**.

如果您需要在帮助下完成Android Studio的安装和创建第一个工程，可以参考 [Android Studio documentation](https://developer.android.com/studio/intro/index.html).

### 设置模拟器

有了Android Studio, 您就可以在开发的同时在您的电脑上设置Android模拟器来测试您的应用。为了设置好模拟器，点击Android Virtual Device (AVD) Manager图标 <img src="/help/img/android/first-steps-avd.png" alt='icon for AVD in the Android Studio interface' />， 然后点击 **Create Virtual Device** 按钮。您也可以在工具栏通过 `Tools` > `Android` > `AVD Manager` 找到AVD Manager。在 **Phones** 类别下，选择 **Nexus 5X** 并点击 **Next** 。选择您想要测试的版本（本教程使用API级别26）。

您可以通过 [Android Studio documentation](http://developer.android.com/tools/help/avd-manager.html) 学习更多设置AVD的方法。

## 安装Mapbox Maps SDK（Android）

在您开始开发您的应用之前，参考 [安装教程](https://www.mapbox.com/install/android/) 安装Mapbox Maps SDK（Android）。安装教程默认您已经下载了Android Studio并创建了一个新的工程，为了成功安装好Mapbox Maps SDK（Android），您将会在您的工程中修改四个不同的文件。 这四个文件包括：

- `build.gradle (Module:App)`: Android Studio使用Gradle来编译资源和源代码成为Android应用程序包文件（APK）。这个纯文档的文件被用来配置编译并列出所有依赖，其中包括Mapbox Maps SDK（Android）。
- `AndroidManifest.xml`: 这是描述应用组成的地方，包括Mapbox相关的许可。
- `MainActivity.java`: 这是一个Java文件，您将在这个文件中编些Mapbox类和函数。
- `activity_main.xml`: 这是您将设置您的MapView属性以及添加标记的地方。

一旦您完成了 [安装指南](https://www.mapbox.com/install/android/) 的所有步骤，这四个文件应该包含如下：

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>build.gradle (Module:App)</div>
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
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,12],
      [17,34],
      [50,97]
    ]}
  />
}}

{{
    <Note title='解决Android Studio错误' imageComponent={<BookImage />}>
        <p>如果您遇到了其它与Mapbox无关的Android Studio错误, 我们推荐您参考 <a href='https://developer.android.com/studio/intro/index.html'>Android Studio documentation</a> 或者在 <a href='https://stackoverflow.com/questions/tagged/android-studio'>StackOverflow</a> 上搜索错误信息。</p>
    </Note>
}}

### 设置MapView

您可以在activity的布局文件中设置多种地图特性，包括初始相机位置或者指南针的屏幕位置。用以下代码替换您在安装过程中在 `activity_main.xml` 文件中添加的代码，地图的中心将重新定位于芝加哥，改变地图间距，放大缩放比例：

{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
  />
}}

Mapbox Maps SDK（Android）附带了一系列地图样式。您可以在Mapbox SDK的 `Style` 类中找到现有的附带样式及其常量。在本例中，您将使用Mapbox的Light样式。

您 _必须_ 用 `MapboxMap` 类的 `setStyle();` 函数通过编程实现地图样式的设置。在 `onMapReady()` 中运行 `mapboxMap.setStyle()` ， `setStyle()` 函数的第二个参数是当地图准备好接收地图相关的代码时加载样式的回调函数：

```java
mapView.getMapAsync(new OnMapReadyCallback() {
@Override
public void onMapReady(@NonNull MapboxMap mapboxMap) {
mapboxMap.setStyle(Style.MAPBOX_STREETS, new Style.OnStyleLoaded() {
	  @Override
	  public void onStyleLoaded(@NonNull Style style) {
	    // Map is set up and the style has loaded. Now you can add data or make other map adjustments
	  }
	});
	}
});
```

您也可以在 `onMapReady()` 函数外部使用 `mapboxMap.setStyleUrl()` ：

```java
mapView.getMapAsync(new OnMapReadyCallback() {
  @Override
  public void onMapReady(MapboxMap mapboxMap) {
      MainActivity.this.mapboxMap = mapboxMap;
  }
});
```

`MainActivity` 中接近最上面的对象 `MapboxMap` 与当XML布局中地图准备好时返回的对象 `MapboxMap` 是相同的。现在您可以在您的 `MainActivity` 代码中任意地方运行 `mapboxMap.setStyle()` 。

{{ <Note title='Creating your own styles' imageComponent={<BookImage />}> }}

<p>您可以用 <a href='https://www.mapbox.com/mapbox-studio/'>Mapbox Studio</a> 创建自定义样式并将其添加到您的应用中。要用代码实现添加一个自定义样式到您的 <code>mapboxMap</code>, 找到您的 <a href='https://www.mapbox.com/studio/styles/'>样式页面</a>, 复制这个样式的 <a href='/help/glossary/style-url/'>样式URL</a>, 然后用 <code>setStyleUrl();</code> 将其添加到您的 <code>mapboxMap</code> 对象中:</p>

```java
mapboxMap.setStyle(new Style.Builder().fromUrl("mapbox://styles/your-mapbox-username/your-style-ID"), new Style.OnStyleLoaded() {
  @Override
  public void onStyleLoaded(@NonNull Style style) {

  }
});
```

{{</Note>}}

请参考 [Mapbox Maps SDK for Android documentation](https://www.mapbox.com/android-docs/map-sdk/overview/#mapview-xml-attributes) 了解可设置 `MapView`的所有XML属性。请随心定义您的地图吧！

### 导入类

当您完成上述代码后，您会发现一些Android Studio发出的红色警告。这是因为您还没有导入在 `MainActivity.java` 中引用的类。

您可以通过按 <kbd class='txt-kbd'>Alt</kbd>+<kbd class='txt-kbd'>Enter</kbd> (Mac电脑使用 <kbd class='txt-kbd'>Option</kbd>+<kbd class='txt-kbd'>Return</kbd>) 自动导入这些类。或者，您可以手动添加以下类到您的 `MainActivity.java` 文件，在 `public class MainActivity extends AppCompatActivity` 上面的任意位置添加即可：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [13,15]
    ]}
  />
}}

点击 **Run 'app'** 按钮 <img src="/help/img/android/first-steps-run.png" alt="icon for running the app in Android Studio" />(或者在Mac电脑上用 <kbd class='txt-kbd'>Control</kbd>+<kbd class='txt-kbd'>R</kbd>) 来运行您的应用。


如果没有错误，Android Studio将会花数秒来运行您的应用。您可以在您之前设置好的Android模拟器中测试它。不管您使用哪个方法，结果应该是一致的––––您应该可以看到初始地图样式被替代成了Mapbox Light样式。

<div class='align-center'>
<img src='/help/img/android/first-steps-change-style.png' alt='screenshot of a virtual Android device displaying a map using the Mapbox Light style' class='inline wmax360'>
</div>

## 添加地图标记

接下来，您将会在地图上添加标记。在您的 `MainActivity.java` 文件中，在紧接着 `mapView.onCreate(savedInstanceState);` 后面但仍然在 `public void onStyleLoaded(@NonNull Style style) { ...});` 内添加以下代码。这样，等到地图加载完成后，一个地图标记将会被添加到特定位置。

一旦样式被设置成Mapbox Light，您添加一个图标图片到地图中，然后在地图中添加 `SymbolLayer` 时用这个图标。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [35,48]
    ]}
  />
}}

重新运行您的应用，一个红色的标记应该会出现。

<div class='align-center'>
<img src='/help/img/android/android-first-steps-intro.png' alt='map with marker on an Android device' class='inline wmax360'>
</div>

## 最终成品

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## 下一步

您成功用Mapbox创建了一个小型Android应用了！您现在可以创建一个Android Studio工程，安装Mapbox Maps SDK（Android），改变地图样式。您可以通过以下资源了解Mapbox的最新信息：

* [Mapbox Maps SDK for Android documentation](https://docs.mapbox.com/android/maps/overview)
* [Mapbox Maps SDK for Android examples](https://docs.mapbox.com/android/maps/examples)
* [Mapbox GL Native on GitHub](https://github.com/mapbox/mapbox-gl-native) ––––关注Mapbox移动端的开源项目。

您也可以 [下载并探索我们的Android展示应用](https://play.google.com/store/apps/details?id=com.mapbox.mapboxandroiddemo&hl=en) 来学习在Android项目中可以使用的所有方法。

