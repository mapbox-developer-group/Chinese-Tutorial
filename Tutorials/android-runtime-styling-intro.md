---
title: 安卓开发中的实时样式更新
description: 通过用户交互和其他“实时”设置更改地图的各种属性
thumbnail: androidRuntimeStyling
level: 2
topics:
- mobile apps
language:
- Java
prereq: An Android application with a map view set up and familiarity with Android Studio and Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-runtime-styling.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial

---

[Runtime Styling](/help/glossary/runtime-styling/) 是安卓开发中Mapbox Maps SDK里的一个强大功能，它能帮助您实现地图属性的实时更新，改变地图样式中方方面面的细节。

在本次教程中，您将会在指引下制作一幅安卓应用平台上的地图，并更改地图中水的填充颜色以及一些海洋标注的文本的样式（字号、颜色、光晕模糊等）。

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-dark-blue-water-adjusted-labels.png' alt='map with water fill color and marine label texts updated on an Android device' class='inline wmax360-mm wmax-full'>
</div>

## 操作准备

完成这个教程需要您对Java语言有所熟悉并有使用Android Studio的经验。下面是一些在教程开始前您需要准备的材料：

- **Mapbox账号和access token**。登录您的Mapbox账号 [mapbox.com/signup](https://www.mapbox.com/signup/)。您可以在 [Account page ](https://www.mapbox.com/account)页面中找到您的 [access tokens](/help/how-mapbox-works/access-tokens/)。请将access token添加到您的
  strings.xml文件中。
- **能加载Mapbox Maps SDK的安卓应用程序**。本教程默认您已经开始开发能使用Mapbox Maps SDK的安卓应用程序。如果您还不熟悉如何使用安卓Maps SDK，请参考 [使用配适安卓的Mapbox Maps SDK指南](/help/tutorials/first-steps-android-sdk/) 设置地图视图。

## 添加设计库

Android Studio使用Gradle工具包将资源和源代码编译到APK中。`build.gradle` 文件用于配置构建和列表依赖项，包括Mapbox Maps SDK。向您的 `build.gradle` 文件中添加安卓设计支持库作为依赖项。这个库不需要使用实时样式，将它添加到应用程序中是为了在这次教程案例中可以使用浮动操作按钮。

```groovy
// in addition to the rest of your build.gradle contents
// you should include the following repository and dependency

repositories {
    mavenCentral()
}

dependencies {
    // Add other library dependencies such as the Mapbox Maps SDK for Android
    implementation 'com.android.support:design:27.1.1'
}
```

您需要在 `activity_main.xml` 文件中设置MapView的属性，以及在地图布局中添加按钮。在此之后点击此按钮将会实时改变样式。在 `app` > `res` > `layout` > `activity_main.xml` 文件中设置初始化应用程序时地图视图的中心，缩放级别和地图样式。

{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
  />
}}

您需要在 `strings.xml` 文件中储存您的access token。文件路径为：`app` > `res` > `values` > `strings.xml`：

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>strings.xml</div>

}}

```xml
<string name="access_token" translatable="false">{{ <UserAccessToken /> }}</string>
```

`MainActivity.java` 是一个Java文件，您可以在其中指定特定于Mapbox的交互。在 `app` > `java` > `yourcompany.yourproject` > `MainActivity.java` 中初始化你的地图：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,11],
      [18,37],
      [58,105]
    ]}
  />
}}

您可以在 [使用配适安卓的Mapbox Maps SDK指南](/help/tutorials/first-steps-android-sdk/) 中了解如何使用适用于安卓的Maps SDK设置Android Studio项目。打开应用程序后，您可以看到以墨西哥湾和加勒比海为中心的Mapbox Streets样式的地图。

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-before.png' alt='a map centered on the Caribbean with Mapbox Streets style an Android device' class='wmax360'>
</div>



## 获取图层

接下来您将使用Mapbox Maps SDK for Android中的代码来获取地图的图层。改变视觉效果的核心其实是控制图层。

### 导入要素类

首先，向 `MainActivity.java` 文件中加载正确的类。`Layer` 类用装载稍后将被控制的图层对象。使用 `PropertyFactory` 类可以更改地图图层的颜色和标注的属性。

添加在 `MainActivity.java` 文件里 `public void onStyleLoaded(@NonNull final Style style) { ... }` 方法中的代码如下：

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [13,13],
      [38,38]
    ]}
  />
}}

## 更改图层样式

接下来您将更改水图层的颜色和几个海洋标注文本的属性。在本教程中，您可以单击粉红色控制按钮来控制更改。

### 导入要素类

在 `MainActivity.java` 文件中导入正确的类。`View` 类用于粉红色控制按钮的点击监听器。您可以在 `Color` 类中使用十六进制颜色代码来设置地图图层的新颜色。

### 更改水的颜色

首先在 `water Layer` 图层对象下添加控制按钮单击监听器，然后将 `onClick（）` 方法内的水色调整为深蓝色。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [15,16],
      [39,45],
      [57,57],
    ]}
  />
}}

请重新打开您的应用程序，单击粉红色控制按钮，您将看到所有地球水的颜色变成深蓝色。

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-dark-blue-water-only.png' alt='a map with dark blue colored water on an Android device' class='wmax360'>
</div>



### 更改海洋标注的文字属性

现在需要您指定新的水标注文本属性。在控制按钮 `onClick()`方法中，添加以下代码来调整标签的光晕模糊、大小、颜色和不透明度。

`for（Layer singleMapLayer：mapboxMap.getLayers（））` 行用于控制应用程序检查每个地图图层的文本 `water -`。这是因为Mapbox Streets样式有几个不同的与水相关的图层ID：

- `water-point-label`
- `water-line-label`

您可以使用 `for` 循环检索这些图层，而不是先用_each_ 给每个水的标注图层创建单独的对象，在对每个单独图层的文本重复更改。您可以使用 `for `循环更改包含相同单词的多个图层的属性，例如 `building`、 `water`、或者 `bridge` 等在层名称中通常重复的单词。

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [46,55]
    ]}
  />
}}

{{<Note title='Layer IDs' imageComponent={<BookImage />}>}}

您需要图层的名称（i.e. ID）来在运行时更改图层的样式。可以在Mapbox Studio中打开样式来查找地图样式（包括我们的Mapbox模板样式）的图层ID。确保您已登录到Mapbox帐户，然后访问 <a href='https://www.mapbox.com/studio/styles/'>Styles page</a> 页面。在帐户的样式列表中找到样式，然后单击其“Edit”按钮。您可以在Mapbox Studio样式编辑器中的左侧边栏中看到列出的地图样式图层。

或者您可以使用MapboxMap类中的 [`getLayers()`](https://www.mapbox.com/android-docs/api/map-sdk/{{constants.VERSION_ANDROID_MAPS}}/com/mapbox/mapboxsdk/maps/MapboxMap.html#getLayers) 方法来获得Android Studio Logcat控制台里每个图层的ID。在 `mapView` 对象的 `onMapReady` 方法中添加以下 `for` 循环代码来获得ID：

```java
for (Layer singleMapLayer : mapboxMap.getLayers()) {
  Log.d("MainActivity", "onMapReady: layer name = " + singleMapLayer.getId());
}
```

现在您已获得图层ID的完整列表，您将知道在运行时可以设置哪些图层样式！

{{ </Note> }}

重新运行您的应用程序，单击粉红色控制按钮，您将看到地图的水图层文本变得更大、更绿、透明度更低，并且具有模糊的光晕。

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-dark-blue-water-adjusted-labels.png' alt='map with attribute styled in runtime on an Android device' class='inline wmax360'>
</div>

## 完成的产品

恭喜您成功创建了一个地图应用程序，并且可以更改水图层的填充颜色与多个图层的文本属性。这些样式更新并不需要改变底层数据集、地图样式或者其他因素，而是在程序运行过程中实时更新！

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-final.gif' alt='map with attribute styled in runtime on an Android device' class='inline wmax360'>
</div>

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## 下一步

使用实时样式更新能够为安卓应用程序创建漂亮且信息丰富的地图。您可以在我们的 [Map design](/help/how-mapbox-works/map-design/) 设计指南中了解更多关于实时样式更新的内容，深入研究一些专门针对安卓的实时样式更新示例：

- [Switch map language](https://github.com/mapbox/mapbox-android-demo/blob/83a0b3c18f56cc549d68a28f23e3c2026e904e7c/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/styles/LanguageSwitchActivity.java)：点击按钮即可更改地图文本的语言。
- [Update by zoom level](https://github.com/mapbox/mapbox-android-demo/blob/eadaf3a81c01f1390753dbe24b560f77d117ec27/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/styles/ZoomDependentFillColorActivity.java)：根据地图的缩放级别更改水图层的颜色。
