---
title: Build a store locator for Android
description: Build a store locator to integrate into an Android application.
level: 3
topics:
- mobile apps
language:
- Java
prereq: Familiarity with Android Studio and Java.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial

---

本指南将指导您如何使用我们的 **Android Store Locator 入门套件**，创建可以集成到任何Android应用程序中的自定义地点定位器地图。您将能够浏览多个店面的位置，选择特定的店面以查看更多信息，获取行程的预估距离和从用户位置到任一店面位置的路线。您可以从五种不同风格的地图中的选择其中一个开始，然后定制店面的位置、店面的标记图标和单个店面信息卡上的所有内容。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-intro.gif' alt='simulation of user interaction with a store locator application' class='inline wmax360-mm wmax-full'>
</div>

<br>

## 准备

以下是开始为Android构建商店定位器所需的内容：

- **Starter kit files**。从GitHub下载或克隆 [Android Store Locator 入门套件](https://github.com/mapbox/store-locator-android/)。这包括功能Android Studio项目的所有必要文件。
- **Android Studio 3.0**。您需要将入门工具包文件与3.0或更高版本的 [Android Studio](https://developer.android.com/studio/index.html) 一起使用。如果您尝试运行应用程序并接收到 `Error running android: Gradle project sync failed. Please fix your project and try again`，请确保您使用的是3.0或更高版本的Android Studio。
- **Mapbox access token**。您将使用 [access token](/help/glossary/access-token) 将地图与您的帐户相关联，您可以在 [Account page](https://www.mapbox.com/account/) 上找到它。
- **一部Android设备（实体机或者模拟器）**。 您需要Android实体机或 [Android模拟器](https://www.mapbox.com/account/) 来预览地点定位器功能。*注意：设备的Android SDK版本号必须为 [16（“Jelly Bean”）或更高版本](https://source.android.com/source/build-numbers)。*
- **可选：Android Drawable Importer**。如果您计划将自定义图像添加到应用程序（例如，可自定义的店面位置图标），请安装 [Android Drawable Importer](http://www.javahelps.com/2015/02/android-drawable-importer.html) 插件以将图像添加到项目中。
- **可选：SVG 编辑工具**。如果您想创建自定义布局或图标，可以使用  [Sketch](http://sketchapp.com)，[Figma](http://figma.com) 或Adobe Illustrator等程序。

## 配置入门工具包

从GitHub下载 [Android Store Locator入门套件](https://github.com/mapbox/store-locator-android/) 后，在Android Studio 3.0 Beta中打开该项目。在项目中，您将找到整个应用程序的所有源文件，包括：

- 5个地图UI主题的变量值。
- 存有店面位置信息的示例GEOJSON数据。
- 使用 [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) 检索路径并在地图上显示为导航路线的代码。

### Access token

在运行应用程序之前，您需要将Mapbox [access token](/help/glossary/access-token) 添加到strings.xml文件中。你可以在目录 `app` > `src` > `main` > `res` > `values` 中找到该文件。

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>strings.xml</div>

}}

```xml
<!-- Add your Mapbox access token between >< in the line below. Your token can
be retrieved at https://www.mapbox.com/account/
-->
<string name="access_token" translatable="false">{{ <UserAccessToken /> }}</string>
```

### `MapActivity`

该 `MapActivity.java` 文件是您调整代码的主要位置。 这个activity可以通过导航工具栏的 `app` > `src` > `main` > `java` > `com` > `mapbox` > `storelocator` > `activity` 找到。使用该文件您可以对应用定制这些：

- 选择地图默认主题。
- 设置地图样式的URL。
- 定制标记图标。
- 根据需要自定义其他UI要素和颜色。

{{
  <Note imageComponent={<BookImage />}>
    <p>The starter kit files include detailed inline comments that tell you what customizations are possible.</p>
  </Note>
}}

## 选择地图主题风格

配置入门工具包后，首先配置一个主题。除非进行调整，否则当应用程序启动时，theme picker activity将在您应用启动时首先显示，然后需要通过单击我们的移动设计师制作的五个主题之一的预览图像来选择主题。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-select-theme.png' alt='screenshot of the theme picker screen of the store locator starter kit application' class='wmax360'>
</div>

选择主题后，请在将 `MapActivity.java` 文件添加到最终应用之前删除theme picker activity:

- 删除文件 - `ThemePickerActivity.java` 和 `MapActivity.java` 文件在同一个目录（`app` > `src` > `main` > `java` > `com` > `mapbox` > `storelocator` > `activity`）。
- 将 `ThemePickerActivity` 从应用程序的manifest文件中删除并将launcher intent filter配置到 `MapActivity`（或者应用程序启动时首先打开的任何其他activity）:

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>Manifest.xml</div>

}}

```xml
<intent-filter>
    <action android:name="android.intent.action.MAIN"/>
    <category android:name="android.intent.category.LAUNCHER"/>
</intent-filter>
```

- 调整 `MapActivity.java` 文件，不再使用 `chosenTheme` 通过 `getIntent().getIntExtra(*SELECTED_THEME*, R.style.*AppTheme_Blue*);` 的方法初始化。相反，将其设置为您选择的主题：

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>MapActivity.java</div>

}}

```java
chosenTheme = R.style.YOUR_CHOSEN_THEME; // Example of a theme: AppTheme_Blue
```

完成这些更改后，请再次运行您的应用。您会看到您指定的风格地图和一些店面分布的位置。在下一步中，您将添加自己的数据和点位位置信息。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-blue-theme.png' alt='screenshot of the android store locator application after the blue theme is chosen' class='wmax360'>
</div>

## 添加您的数据

入门工具包包含一个GeoJSON文件 `list_of_locations.geojson`，您可以在其中找到当前地图上所有可见的店面位置。[GeoJSON](/help/glossary/geojson/) 是地理空间数据的文件格式和JSON格式的子集。在本部分中，您将更新示例数据以反映您实际店面的位置。

`list_of_locations.geojson `文件位于 `app` > `src` > `main` > `assets`。查看数据的组织形式。请注意，每个商店位置都是GeoJSON文件中独立的要素。每个要素都有四个 `properties` 描述有关商店位置的一些特征，`geometry` 指明该要素是单个点以及该点在整个于世界中的坐标。

您可以使用自己的店面位置数据替换示例数据。如果您有以GeoJSON格式的数据，可以删除当前数据并将其替换为您自己的数据。*注意：如果数据包含的数据 `properties` 与默认数据不同，则需要更新 `MapActivity.java` 文件和 `LocationRecyclerViewAdapter` 类中的相关代码。*我们建议使用 [geojson.net](http://geojson.net/) 快速验证和可视化您的GeoJSON。

如果您没有GeoJSON格式的店面数据，则可以使用Mapbox Studio dataset editor创建新的GeoJSON文件。在此示例中，您将使用 [Mapbox Studio dataset editor](https://www.mapbox.com/studio/datasets) 为俄亥俄州哥伦布市的 [Jeni's Splendid Ice Cream](https://jenis.com/about/) 位置创建一个数据集，导出GeoJSON文件，替换GeoJSON数据 `list_of_locations.geojson`，然后调整数据的bounding box，模拟用户的位置，再次运行您的应用程序查看新的店面位置。

### 创建数据集

_如果您已有商店位置的GeoJSON文件，则可以跳到 [替换数据](#r替换数据) 部分。_

有几种方法可以创建新的GeoJSON文件。在本指南中，您将使用 [Mapbox Studio dataset editor](https://www.mapbox.com/studio-manual/reference/datasets/#dataset-editor)，这是一个便于上手的浏览器内应用程序，用于创建和编辑Mapbox [数据集](/help/glossary/dataset/)。在本指南中，您将使用Jeni的已知位置，添加您的店面位置信息到数据集并且能够搜索。

首先，创建一个新的数据集:

1. 登录 [Mapbox Studio](https://www.mapbox.com/studio) 并导航到 [数据集页面](https://www.mapbox.com/studio/datasets)。
2. 单击**新建数据集**按钮。
3. 将会打开一个新窗口。您会使用右上角的**空白数据集**选项。
4. 将数据集命名为“ice-cream“，然后单击**新建**。 
5. 数据集编辑器将自动打开。

接下来，您将开始添加店面。您可以使用数据集编辑器中的地理编码器搜索定位区域，使用绘图工具向数据集添加新的点位。您可以使用数据集编辑器的绘图工具更改现有要素的几何形状，位置和附加属性。

1. 在**搜索地址**表单内单击并输入`3998 Gramercy St, Columbus, Ohio`。
2. 在搜索结果中单击与您搜索相匹配的地址。
3. 单击**添加到数据集**按钮，将该地址添加到数据集中。
4. 单击新加的这个要素，左侧属性列表里给它添加如下的属性信息：

- 将 `place_name` 字段更改为 `description`。
- 添加字段名称 `name` 并为其指定值 `Easton`。
- 添加字段名称 `hours`并 为其指定值 `11 a.m. to 11 p.m.`。
- 添加字段名称 `phone` 并为其指定值 `614-476-5364`。

您可以针对每个已知的店面地址逐个执行此过程。添加完每个店面的位置后，您可以**保存**，返回 [数据集页面](https://www.mapbox.com/studio/datasets)，单击“ice-cream”名称的数据集旁边的{{<Icon name='menu' inline={true} />}}按钮，单击**下载GeoJSON**。

为了节省时间，对于本指南，我们在下面提供了完整的GeoJSON供您在下一步中使用：

```json
{
  "features": [
    {
      "type": "Feature",
      "properties": {
        "description": "3998 Gramercy St, Columbus, Ohio 43219, United States",
        "name": "Easton",
        "hours": "11 a.m. to 11 p.m.",
        "phone": "614-476-5364"
      },
      "geometry": {
        "coordinates": [
          -82.917665,
          40.051791
        ],
        "type": "Point"
      },
      "id": "address.11780104298749790"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "714 N High St, Columbus, Ohio 43215, United States",
        "name": "North Market",
        "hours": "10 a.m. to 5 p.m.",
        "phone": "614-228-9960"
      },
      "geometry": {
        "coordinates": [
          -83.00418,
          39.971888
        ],
        "type": "Point"
      },
      "id": "address.1504101080777130"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "900 Mohawk St, Columbus, Ohio 43206, United States",
        "name": "German Village",
        "hours": "Noon to 10 p.m.",
        "phone": "614-445-6513"
      },
      "geometry": {
        "coordinates": [
          -82.992495,
          39.944236
        ],
        "type": "Point"
      },
      "id": "address.18662160207305960"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1 W Bridge St, Dublin, Ohio 43017, United States",
        "name": "Dublin",
        "hours": "11 a.m. to 11 p.m.",
        "phone": "614-792-5364"
      },
      "geometry": {
        "coordinates": [
          -83.114164,
          40.099224
        ],
        "type": "Point"
      },
      "id": "address.3847501076015100"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "2156 E Main St, Columbus, Ohio 43209, United States",
        "name": "Bexley",
        "hours": "11 a.m. to 11 p.m.",
        "phone": "614-231-5364"
      },
      "geometry": {
        "coordinates": [
          -82.941956,
          39.957461
        ],
        "type": "Point"
      },
      "id": "address.5795414383633980"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "714 N High St, Columbus, Ohio 43215, United States",
        "name": "Short North",
        "hours": "11 a.m. to 11 p.m.",
        "phone": "614-294-5364"
      },
      "geometry": {
        "coordinates": [
          -83.003353,
          39.976965
        ],
        "type": "Point"
      },
      "id": "address.748502797349860"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "160 S High St, Columbus, Ohio 43215, United States",
        "name": "The Commons",
        "hours": "11 a.m. to 8 p.m.",
        "phone": "614-867-5512"
      },
      "geometry": {
        "coordinates": [
          -82.999991,
          39.958812
        ],
        "type": "Point"
      },
      "id": "address.7894313840035430"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1281 Grandview Ave, Columbus, Ohio 43212, United States",
        "name": "Grandview Heights",
        "hours": "11 a.m. to 11 p.m.",
        "phone": "614-488-2680"
      },
      "geometry": {
        "coordinates": [
          -83.045003,
          39.983947
        ],
        "type": "Point"
      },
      "id": "address.8328248295013750"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "8 N Liberty St, Powell, Ohio 43065, United States",
        "name": "Powell",
        "hours": "11 a.m. to 11 p.m.",
        "phone": "614-846-1060"
      },
      "geometry": {
        "coordinates": [
          -83.074985,
          40.158137
        ],
        "type": "Point"
      },
      "id": "address.8508074803994320"
    }
  ],
  "type": "FeatureCollection"
}
```

### 替换数据

打开 `list_of_locations.geojson` 文件。删除当前内容并添加上一步中的GeoJSON数据。示例代码和此示例中提供的数据包含每个商店位置的四个属性:

- `name`
- `description`
- `hours`
- `phone`

由于所有要素的 `properties` 和初始GeoJSON数据都是上面的四个属性名称，因此您的地图将立即完全正常运行。如果您希望显示和 `properties` 区别的字段信息，则需要更改 `MapActivity.java` 文件和`LocationRecyclerViewAdapter` 类中的相关代码。

### 更新边界框和位置

该 `MapActivity.java` 文件在应用程序时初始化地图时指定了以纽约为中心。使用以下代码段替换当前代码以将地图中心更改到俄亥俄州哥伦布市。

首先，应用程序初始化的过程中，配置文件 `app` > `res` > `layout` > `activity_map.xml`，设置目标经纬度为哥伦布市所在的经纬度。

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>activity_map.xml</div>

}}

```xml
mapbox:mapbox_cameraTargetLat="39.95"
mapbox:mapbox_cameraTargetLng="-83"
```

然后，更改 `MapActivity.java` 文件中的边界框，以便打开地图，可以显示整个的哥伦布市。

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>MapActivity.java</div>

}}

```java
private static final LatLngBounds LOCKED_MAP_CAMERA_BOUNDS = new LatLngBounds.Builder()
    .include(new LatLng(40.1746, -83.1426))
    .include(new LatLng(39.9278, -82.8814))
    .build();
```

最后，在 `MapActivity.java` 文件中将模拟的用户位置更改为哥伦布市附近。

{{

  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>MapActivity.java</div>

}}

```java
private static final LatLng MOCK_DEVICE_LOCATION_LAT_LNG = new LatLng(40, -83);
```

运行该应用程序，您将看到俄亥俄州哥伦布市显示在地图中心。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-custom-data.png' alt='screenshot of the android store locator application after store location data is updated' class='wmax360'>
</div>

### 显示距离和路线

入门套件使用 [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) 显示预估的行程距离和路线。一旦您更改了GeoJSON数据里的店面信息或者模拟的用户地址，Mapbox Directions API将自动读取您的GeoJSON文件，以检索任一店面到您某个位置的距离和路线。可以在 `MapActivity.java` 文件中找到指定如何使用Directions API的代码。

## 添加自定义标记

您可以将任何图像用作标记——您可以使用emoji（如入门工具包文件中），自己创建的图标，公司的logo或者多个来自开源资源的图标。建议查找使用以下图标资源用于标记：

- Mapbox 的 [Maki icons](https://www.mapbox.com/maki/) 
- [Flat Icon](http://flaticon.com)
- [Get Emoji](http://getemoji.com)

在本指南中，您将使用来自开源项目Flat Icon中的图标。此图标由 <a href="https://www.flaticon.com/authors/eucalyp" title="Eucalyp">Eucalyp</a> 从<a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com </a>制作，由 <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a> 许可。您可以下载该图标的一个白色版或从 [Flat Icon](https://www.flaticon.com/)下载另一个图标。**使用Flat Icon中的图标时，请务必妥善记入作者。**

[{{<Icon name='arrow-down' inline={true} />}} Download the icon on a white marker](/help/data/new-ice-cream-icon.png)

如 [准备](#准备) 所述，我们建议安装并使用 [the Android Drawable Importer](http://www.javahelps.com/2015/02/android-drawable-importer.html) 插件将图像添加到项目中。此插件会自动缩放图像并将图像添加对应屏幕大小的文件夹里（MDPI，XHDPI，XXHDPI等）。

### 将新图像添加到项目中

安装Android Drawable Importer插件，下载你想用来标记店面位置的图像以后，将该图像添加到 `app` > `res` > `drawable `文件夹。右键单击**drawable**文件夹，将鼠标悬停在**New**菜单项上，在子菜单里选择**Batch Drawable Importer**。*注意：此选项仅在安装Android Drawable Importer后可用*。

![screenshot of the menu you will need to navigate to add an image using the Batch Drawable Importer](/help/img/android/android-store-locator-add-image.png)

在打开的窗口中，单击 **+** 并选择您的文件。另一个窗口将打开。在这个窗口中，记下分配给图像的 *Target-name*。对于指南，请使用名称 `new_ice_cream_icon` 并单击**Ok**。在第一个窗口中，您也可以单击**Ok**。

请注意，`drawable` 文件夹中添加了一个新文件夹。来自刚才的导入程序的*Target-name* ，名称是*new_ice_cream_icon*，它包含多个文件——针对各种屏幕大小进行优化的新图像。

![screenshot of the folder for your new image and the files it contains](/help/img/android/android-store-locator-batch-image.png)

### 使用新图像做标记

现在您已成功导入新图像。修改代码指定那张图片用来标记所有的店面位置，指定标记位置图片的代码在 `MapActivity.java` 里。要将图像更改为 `new_ice_cream_image`：

1. 打开 `MapActivity.java`。
2. 查找 `private void initializeTheme() { }`。
3. 在该方法中，找到 `case R.style.AppTheme_Blue:`。这是指定标记、路径和模拟用户位置样式的代码。
4. 对于 `unselectedMarkerIcon` 和 `selectedMarkerIcon` 将 `R.drawable.ice_cream_icon` 改成 `R.drawable.new_ice_cream_icon`。

再次运行应用程序，您会看到所有的商店位置都是冰淇淋图标。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-custom-icon.png' alt='screenshot of Store Locator application with the new ice cream icon as markers' class='wmax360'>
</div>

## 自定义信息卡图标

除了自定义地图外观外，您还可以为每个店面定制信息卡片的样式。接下来，您将更改滚动信息卡上显示的图标。这个例子从一个非常棒的开源项目 [Unsplash](https://unsplash.com/) 里，找到一个孩子正在享用的冰淇淋图标。原始图像已被裁剪并修改为105px x 105px的图像尺寸。

[{{<Icon name='arrow-down' inline={true} />}} Download the image](/help/data/ice-cream-kid.jpg)

### 导入图像

按照 [上一节](###使用新图像做标记) 中描述的相同过程，使用Android Drawable Importer插件将新的滚动信息卡图像添加到项目中。使用*Target-name* 为 `ice_cream_kid`。

### 使用滚动信息卡上的新图像

现在您已成功导入新图像，请更改代码指定滚动信息卡中应用的图像。信息卡的代码存在于 `single_location_map_view_rv_card.xml` 布局文件中。在此文件中，您可以调整卡片上不同元素的样式（包括间距，位置和大小）。单个店面信息卡的页面布局信息将提供给 `ReyclerView.java` adapter，此adapter最终会在设备屏幕底部创建可滚动的卡列表。

改动滚动信息卡的图像，需要将您想要使用的 `drawable` 文件，在 `LocationRecyclerViewAdapter `类文件的 `onBindViewHolder()` 方法里，传递给 `emojiForCircle` 初始化:

1. 打开 `app` > `java` > `adapter `文件夹下的 `ReyclerView.java`。
2. 找到 `switch (selectedTheme) { }`。
3. 在该方法中，找到 `case R.style.AppTheme_Blue:`。这是用于指定滚动信息卡上显示样式的代码。
4. 设置 `emojiForCircle` 等于 `ResourcesCompat.getDrawable(context.getResources(), R.drawable.ice_cream_kid, null);`
5. 删除 `backgroundCircle = ResourcesCompat.getDrawable(context.getResources(), R.drawable.blue_circle, null);`.

再次运行应用程序，您会在滚动信息卡上看到新的图像。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-custom-card-image.png' alt='screenshot of store locator application with custom scrolling card image' class='wmax360'>
</div>

## 最终成果

您已经了解了Android Store Locator入门套件的工作原理，并修改了地点定位器的一些可自定义的关键元素。

<div class='align-center'>
<img src='/help/img/android/android-store-locator-final-product.gif' alt='simulating user interaction with the final customized store locator' class='wmax360'>
</div>



## 下一步

请查看Mapbox Maps SDK for Android [文档](https://www.mapbox.com/android-docs/) 和 [示例](https://www.mapbox.com/android-docs/map-sdk/examples)，来了解有关自定义地图应用或添加其他功能的更多信息。如果您有兴趣创建自己的自定义地图样式，代替地点定位器入门套件中提供的设计地图主题，请了解如何使用Mapbox Studio通过 [创建自定义样式](/help/tutorials/create-a-custom-style/) 教程来构建适合您品牌的样式。
