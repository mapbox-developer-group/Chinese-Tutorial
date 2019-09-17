刘年华已完成 ios-store-locator.md 文件翻译
@xuewOng

---
title: Build a store locator for iOS
description: Build a store locator that can be integrated into any iOS application.
thumbnail: iosStoreLocator
level: 3
topics:
- mobile apps
language:
- Swift
- Objective-C
prereq: Familiarity with Xcode, Swift, and CocoaPods.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: tutorial
---

这份指南将指引您如何使用我们的**iOS商铺定位入门套件**，创建可集成到任何iOS应用程序中的自定义商铺定位地图。您可以直观地看到许多位置，或者选择特定位置以查看详细信息，以及检索从用户位置到任何商店位置的路线。我们提供了五个主题供您选择，您可以自定义商店位置到图标记号，甚至是每个商店的相关信息。

{{<img alt='animated GIF of a store locator application on an iOS device' src='/help/img/ios/store-locator-final-product.gif' className='wmax360 block mx-auto' />}}

## 入门

iOS商铺定位入门套件可在iOS 9.0及更高版本上运行。它可以与使用Xcode 9在Swift 3.1及更高版本的代码一起运行。下面这些是开始前您需要的资源：

- **入门套件相关文件**. 从Github下载或者复制一份 [iOS Store Locator starter kit](https://github.com/mapbox/store-locator-ios/) 里面包括所有运行Xcode项目的必要文件。
- **Mapbox账号和访问token**. 在Mapbox官网上注册一个账号 [mapbox.com/signup](https://www.mapbox.com/signup/). 您可以查找到访问token [access tokens](/help/how-mapbox-works/access-tokens/) 在您的账户页面 [Account page](https://www.mapbox.com/account/). 您可以将访问token添加至 Info.plist 文件中。
- **能访问iOS系统的硬件或者模拟iOS系统环境 [simulated iOS device](https://help.apple.com/simulator/mac/current/#/deve44b57b2a)**.
- **可选项：SVG编辑工具**. 如果您想创建自定义图标，可以使用 [Sketch](http://sketchapp.com), [Figma](http://figma.com), 或者 Adobe Illustrator 等程序。


## 设置入门套件

在iOS商铺定位入门套件包括所有所需的源文件 [iOS Store Locator starter kit](https://github.com/mapbox/store-locator-ios/)。该套件包括：

- 五个UI主题
- 带有商铺定位的GeoJSON数据相关示例
- 检索路线并在地图上导航的代码 [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) 

### 安装须知

使用 CocoaPods 安装项目所需的程序. 如果你不了解 CocoaPods，请阅读 [CocoaPods documentation](https://guides.cocoapods.org/using/getting-started.html) 。在包含入门套件的目录中运行 `pod update` 这样就能将运行程序所需的程序 (**Mapbox-iOS-SDK** and **MapboxDirections.swift**) 添加到项目中。

运行 `pod update`后, 退出 `mapbox-store-locator.xcworkspace` (不是 `mapbox-store-locator.xcodeproj`)。 `mapbox-store-locator.xcworkspace` 包含了必要的程序。下载好pod后，用命令行输入 `open mapbox-store-locator.xcworkspace/` 

### 添加访问 token

如果希望在 Xcode 9 中打开项目并显示地图, 就需要将访问token添加至 `Info.plist` 文件中。 您可以在个人账户[Account page](https://www.mapbox.com/account/)页面中，找到token访问页面 [access tokens](/help/how-mapbox-works/access-tokens/)，并将访问token添加到项目中:
1. 打开 `Info.plist`.
1. 找到 `MGLMapboxAccessToken`中的 _Key_ 并替换占位符 _Value_,用你的访问token替换 `<Add Access Token>`.

### `ThemeViewController`主题预览

`ThemeViewController.swift` 是自定义的主要位置。通过 `ThemeViewController.swift`文件，您可以：

- 选择一个主题
- 设置地图样式 URL
- 选择标记图表
- 根据需要自定义UI的其他元素和颜色

{{
    <Note
      imageComponent={<BookImage />}
    >
        <p>入门套件相关文件中详细注释了哪些元素是可以自定义的.</p>
    </Note>
}}

## 选择主题

完成入门套件的设置后，选择一个主题，开始自定义应用程序。

### 主题预览

Unless adjusted, the theme picker preview will be the first thing you see when the app is launched. Run your application and browse available themes by clicking on the preview image for one of five themes made by our mobile designers.除非有修改，否则主题选择预览将是您在启动应用时看到的第一个内容。运行应用程序，单击我们的设计师制作的预览图像，即可浏览相关主题。

{{<img alt='animated GIF of a user clicking through to preview various available themes' src='/help/img/ios/store-locator-explore-themes.gif' className='wmax360 block mx-auto' />}}

### 设置主题

本教程将以第五个主题 `neutralTheme`为例。这个主题有 [Mapbox Streets](https://www.mapbox.com/maps/streets/)的样式，每个商铺坐标也有一个房屋的图案标识。通过以下操作来设置这个主题：

1. 打开 `ThemeViewController.swift` 文件
2. 找到 `var viewControllerTheme : Theme?` 并删除这行
3. 找到被注释的一行 `// var viewControllerTheme : Theme? = MBXTheme.purpleTheme`
4. 高亮这行代码，并用 `command` + `/` 取消注释
5. 用 `.purpleTheme` 替代 `.neutralTheme`.

现在已经选择了 the neutral theme 这个主题。但在初始化时，应用程序仍然设置为打开主题预览。接下来，我们来更改这个设置。

### 更改主题预览

1. 打开 `Main.storyboard`
2. 点击 **Theme View Controller Scene**
3. 单击右上角的 Attributes 属性检查
4. 点击 *Is Initial View Controller* 旁边的框

![screenshot of how to set the initial view controller in Xcode](/help/img/ios/store-locator-set-initial-view.png)

运行应用程序，将显示有Mapbox Streets样式并带有多个房屋图标的地图。

{{<img alt='screenshot of a map with several markers on an iOS device using the neutral theme centered on New York City' src='/help/img/ios/store-locator-choose-a-theme.png' className='wmax360 block mx-auto' />}}

## 添加数据

入门套件中包含了一个 GeoJSON 文件叫做 `stores.geojson` ，您可以在其中找到地图上所有当前可见的商店坐标。[GeoJSON](/help/glossary/geojson/) 是地理空间数据的文件格式和JSON格式的子集。这一部分，我们来更新示例数据以显示商店的实际位置。

找到 `stores.geojson` 文件并查看其数据格式。 请注意，每个商铺位置都是一个单独的 GeoJSON _feature_ 文件。每个 feature 有四个 `properties` 来描述有关位置的一些特征, `geometry` 指的是这个 feature 是一个孤点，并且在世界中所处的位置。

如果有 GeoJSON 格式的商店位置数据，可以删除当前数据并将其替换为自己的数据。

### 替换数据

在这份指南中，我们为这一步提供了相关的 GeoJSON 示例。 这个例子中，我们将使用伊利诺伊周动物收容所的相关数据 [animal shelters in Cook County, Illinois](https://datacatalog.cookcountyil.gov/dataset/Area-Animal-Shelters-Map/t86e-hv9w)替换 `stores.geojson` 中的现有数据。然后就可以调整边界框并模拟用户位置来运行应用，以查看新的商店位置。


```json
{
  "features": [
    {
      "type": "Feature",
      "properties": {
        "description": "18736 W Peterson Rd, Libertyville",
        "name": "Lake County Animal Care and Control",
        "hours": "M-F 9am-4:30pm, Sat 9am-12:30pm",
        "phone": "847-377-4700"
      },
      "geometry": {
        "coordinates": [
          -87.998316,
          42.306035
        ],
        "type": "Point"
      },
      "id": "address.10164434706493830"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1103 W End Ave N, Chicago Heights",
        "name": "Animal Care League",
        "hours": "M-F 9am-5pm",
        "phone": "708-848-8155"
      },
      "geometry": {
        "coordinates": [
          -87.79962,
          41.872075
        ],
        "type": "Point"
      },
      "id": "address.11842842831717040"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1375 N Roselle Rd, Schaumburg",
        "name": "Golf Rose Animal Hospital",
        "hours": "M-F 8am-7pm, Sat 9am-2pm",
        "phone": "847-885-3344"
      },
      "geometry": {
        "coordinates": [
          -88.079033,
          42.053136
        ],
        "type": "Point"
      },
      "id": "address.14288456127471660"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1634 S Laramie Ave, Cicero",
        "name": "Waggin Tails",
        "hours": "M-F 1pm-6pm",
        "phone": "708-652-0825"
      },
      "geometry": {
        "coordinates": [
          -87.755487,
          41.85705
        ],
        "type": "Point"
      },
      "id": "address.14994575158876850"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "5127 Oakton St, Skokie",
        "name": "Skokie Animal Control",
        "hours": "not available",
        "phone": "847-933-8484"
      },
      "geometry": {
        "coordinates": [
          -87.71049,
          42.024031
        ],
        "type": "Point"
      },
      "id": "address.15065751370530970"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "10305 Southwest Hwy, Chicago Ridge",
        "name": "Animal Welfare League (AWL)",
        "hours": "M-Sat 9am-9pm, Sun 9am-6pm",
        "phone": "708-636-8586"
      },
      "geometry": {
        "coordinates": [
          -87.787701,
          41.703627
        ],
        "type": "Point"
      },
      "id": "address.17674198339620830"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1103 W End Ave N, Chicago Heights",
        "name": "Paws Tinley Park",
        "hours": "M, W, F 7pm-9pm, T, Th, Sat, Sun 12pm-4pm",
        "phone": "815-464-7298"
      },
      "geometry": {
        "coordinates": [
          -87.806946,
          41.543834
        ],
        "type": "Point"
      },
      "id": "address.5098323152873800"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1103 W End Ave N, Chicago Heights",
        "name": "South Suburban Humane Society",
        "hours": "M, W, F 1pm-7pm, Sat-Sun 12pm-5pm",
        "phone": "708-755-7387"
      },
      "geometry": {
        "coordinates": [
          -87.631074,
          41.511524
        ],
        "type": "Point"
      },
      "id": "address.6529417923998300"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1634 S Laramie Ave, Cicero",
        "name": "DuPage County Animal Hospital",
        "hours": "M, Th 8am-7:30pm, T, W, F 8am-5pm, Sat 10am-3pm",
        "phone": "630-407-2800"
      },
      "geometry": {
        "coordinates": [
          -88.143366,
          41.866063
        ],
        "type": "Point"
      },
      "id": "address.7211235368236180"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1375 N Roselle Rd, Schaumburg",
        "name": "Evanston Animal Shelter & Animal Control",
        "hours": "M-F 8am-7pm, Sat 9am-2pm",
        "phone": "847-866-5082"
      },
      "geometry": {
        "coordinates": [
          -87.6712,
          42.0267
        ],
        "type": "Point"
      },
      "id": "neighborhood.281624"
    }
  ],
  "type": "FeatureCollection"
}
```

为了显示真实的商店坐标，我们需要替换掉 `stores.geojson` 文件中的相关数据。打开 `stores.geojson` 文件，删除掉现有的内容，并有上面的 GeoJSON 数据替代。 示例代码和此示例中提供的数据包含每个商店位置的四个属性：

- `name`
- `description`
- `hours`
- `phone`

只要所有的属性 `properties` 都与初始条件下使用的四个属性相似，这个地图就可以立刻运行了。如果有其他信息希望通过属性 `properties` 来显示，可以更新 `ThemeViewController.swift` 文件中的相关代码 &mdash; 寻找在 `// MARK: Update the attribute keys based on your data's format` 后方注释的代码。

{{
    <Note
      title='从零开始构建一个 GeoJSON 格式数据集'
      imageComponent={<BookImage />}
    >
      <p>有几种方法可以构建 GeoJSON 数据，如果你没有包含商铺信息的 GeoJSON 数据，你可以使用 <a href='https://www.mapbox.com/studio-manual/reference/datasets/#dataset-editor'>Mapbox Studio dataset editor</a> 来编辑。这是一个非常方面的 Mapbox 数据编辑器 <a href='/help/glossary/dataset/'>datasets</a>.</p>
      <p>首先，创建一个数据集:</p>
      <ol>
          <li>登录 Mapbox Studio 并找到 <a href='https://www.mapbox.com/studio/datasets'>Datasets page</a>.</li>
          <li>点击 <strong>新建数据集</strong> 按键.</li>
          <li>一个新窗口将会打开，使用在右上角的 <strong>空白数据集</strong> 选项.</li>
          <li>为数据集命名，并单击 <strong>创建</strong>.</li>
          <li>数据编辑器将会自动打开.</li>
      </ol>
      <p>接下来，开始添加商铺坐标。可以使用数据编辑器中的地理编码器搜索位置，使用绘图工具向数据集添加新点。也可以使用数据编辑器的绘图工具更改现有要素的几何，位置和属性。</p>
      <p>添加完每个位置后，可以 <strong>保存</strong>, 返回 <a href='https://www.mapbox.com/studio/datasets'>Datasets page</a>，点击 数据集旁边的<strong>菜单</strong><Icon name="menu" inline={true} /> 按钮, 然后点击 <strong>下载</strong> 以获取 GeoJSON 数据。</p>
    </Note>
}}

## 模拟用户位置和地图中心

 `ThemeViewController.swift` 文件指定在初始化应用程序以纽约为地图中心。接下来，我们将更新用户的模拟位置到伊利诺伊州库克县。

### 用户位置许可

在地图上绘制用户位置之前，必须征得他们的许可，并简要说明您的应用程序将如何使用他们的位置数据。默认情况下，已在入门套件中配置位置权限。

通过设置  Info.plist 文件中的密钥 `NSLocationWhenInUseUsageDescription`来编辑位置使用说明。我们建议将其中的内容设置为以下字符串，即应用程序的位置使用说明： `Shows your location on the map and helps improve OpenStreetMap`iOS 11要求在 `NSLocationWhenInUseUsageDescription` 的基础上提供 `NSLocationAlwaysAndWhenInUseUsageDescription`。我们建议为此密钥提供不同的字符串，以帮助用户决定应用程序的授权级别。当用户第一次打开应用程序时，系统会向他们显示一条警告，询问他们是否允许应用程序访问其位置。

### 模拟用户位置

在模拟器中运行应用程序时，将看到一个对话框，要求获得使用位置服务的权限。点击 **Allow**。在转到模拟器的菜单栏 **Debug > Location > Custom Location**之前，将无法在地图上看到相关位置。输入 `41.948` 作为纬度坐标， `-87.839` 作为经度坐标，将会看到用户位置出现在库克县。

{{
    <Note
      title='在设备上模拟用户位置'
      imageComponent={<BookImage />}
    >
        <p>如果你在硬件设备上运行程序，而不是通过模拟器，你需要创建一个包含坐标的 GPX 文件 (<code>41.948</code> for latitude, <code>-87.839</code> for longitude)。命名文件 <code>Chicago</code>。然后，使用 <strong>Product > Scheme > Edit Scheme</strong> 将 <em>默认位置更改</em> to <code>Chicago</code>.</p>
    </Note>
}}

最后，调整地图预览级别。通过 `viewDidLoad` 功能，寻找 `mapView.zoomLevel` ，并将其设置为 `8`。

```swift
override func viewDidLoad() {
    ...

    mapView.zoomLevel = 8

    ...
}
```

更新用户位置信息后，Mapbox Directions API 将自动读取 GeoJSON 文件，以检索每个位置的路线。

运行应用程序，将看到以库克县为中心的地图，显示新替代的数据。

{{<img alt='screenshot of a map with several markers on an iOS device using the neutral theme centered on Cook County Illinois' src='/help/img/ios/store-locator-add-data.png' className='wmax360 block mx-auto' />}}

## 添加自定义图标

应用程序将默认使用房屋图标显示每个动物收容所的位置，但使用商铺定位套件，您可以自定义图标，使用任何想要的内容。接下来，我们将当前房屋图标切换为狗图标。

{{<img alt='preview of a selected dog icon' src='/help/img/ios/store-locator-dog-icon-selected.png' className='wmax120 mx-auto block' />}}

### 添加图标

作为图标的图片都将放置在 `Assets.xcassets` 文件夹中。打开文件夹并浏览当前文件，将会看到两个房屋图标 `blue_selected_house` 和 `blue_unselected_house`。右键单击 `blue_selected_house` 并点击 **Show in finder**。

在这种情况下，每个图标都来自同一个文件夹 `blue_selected_house.imageset`。这个文件夹中有两个文件：图像的pdf文件和 [`Contents.json` file](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_ref-Asset_Catalog_Format/ImageSetType.html).

上传两个新的狗图标（一个用于选中图标时，一个用于未选中图标）：

1.下载此压缩包 [this zipped file](/help/demos/ios-store-locator/dog_icon.zip) ，其中包含了两个狗图标。
2.解压并将其添加至项目中 `Assets.xcassets` 文件夹。

### 更改图标引用

接下来，您需要将所有对房屋图标的引用更改为指向狗图标。在 `Themes.swift` 文件中，分别查找对 `blue_selected_house` 和 `blue_unselected_house` 的引用，并用 `blue_selected_dog` 和 `blue_unselected_dog` 分别替代。
```swift
static let neutralTheme = Theme(defaultMarker: UIImage(named: "blue_unselected_dog")!,
    selectedMarker: UIImage(named: "blue_selected_dog")!,
    styleURL: MGLStyle.streetsStyleURL,
    themeColor: ThemeColor.neutralTheme,
    fileURL: Bundle.main.url(forResource: "stores", withExtension: "geojson")!)
```

运行应用程序，将在每个动物收容所的位置看到狗图标。

{{<img alt='screenshot of a map with several markers with dog icons on an iOS device' src='/help/img/ios/store-locator-custom-markers.png' className='wmax360 block mx-auto' />}}

## 自定义信息卡

除了自定义地图和图标外，还可以自定义信息卡，以便在单击时显示有关位置的信息。接下来，您将自定义信息卡上半部分的背景颜色。在 `Themes.swift` 文件中，将当前 `primaryDarkColor` 的 `neutralTheme` 颜色从灰色替换为蓝色:

```swift
static let neutralTheme = Color(primaryColor: UIColor(red:0.91, green:0.90, blue:0.88, alpha:1.0),
    // The line below has been updated from gray to blue
    primaryDarkColor: UIColor(red: 0.2706, green: 0.6667, blue: 0.9098, alpha: 1.0),
    navigationLineColor: UIColor(red:0.00, green:0.73, blue:1.00, alpha:1.0),
    lowerCardTextColor: UIColor.black,
    accentColor: UIColor.white)
```

运行应用程序，单击某个位置，将看到一个蓝色背景的信息卡。

{{
<div className='my12 grid grid--gut12'>
  <div className='col col--6-mm col--12 align-center'>
    <img alt='screenshot of an iOS device with a map with a marker selected displaying an information card with a gray background' src='/help/img/ios/store-locator-custom-card-before.png' className='hmax360' />
    <div><em>Before customizing</em></div>
  </div>
  <div className='col col--6-mm col--12 align-center'>
    <img alt='screenshot of an iOS device with a map with a marker selected displaying an information card with a blue background' className='hmax360' src='/help/img/ios/store-locator-custom-card-after.png' />
    <div><em>After customizing</em></div>
  </div>
</div>
}}

## 最终产品

您已经学习了iOS商铺定位套件的工作原理，并修改了定位的一些可自定义元素。

{{<img alt='animated GIF of a store locator application on an iOS device' src='/help/img/ios/store-locator-final-product.gif' className='wmax360 block mx-auto' />}}

## 下一步

阅读 [Mapbox Maps SDK for iOS documentation](https://www.mapbox.com/ios-sdk/) 和 [examples](https://www.mapbox.com/ios-sdk/examples) 以了解有关自定义应用程序或添加其他功能的更多信息。如果您对创建自定义地图样式来替换iOS Store定位器入门套件中提供的设计器主题感兴趣，请继续阅读 [Create a custom style](/help/tutorials/create-a-custom-style/) 教程，以使用 Mapbox Studio 构建喜欢的主题。
