---
title: Our map data
description: Learn about Mapbox’s map data, where it comes from, and how you can leverage it in your next project.
image: /img/narrative/data.svg
topics:
  - data
prependJs:
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: guide
---

我们模板地图样式中的所有数据皆来自于Mapbox四个地图元件（tilesets）之一。地图元件是一系列在22个预设尺度下以统一矩形图块划分的栅格或矢量数据。

地图元件可由栅格或者矢量图块组成。栅格地图元件包含一系列不同尺度下的影像，它们构成一副完整的地图。 [Mapbox Satellite style](https://www.mapbox.com/maps/satellite/)即由一个栅格地图元件源制作而成。

我们其他的地图样式均使用矢量地图元件制作。矢量地图元件包含几何图形与元数据（如路名、地名、门牌号）的结合体。矢量图块仅在用户（如网页浏览器或移动app）发出请求时进行渲染。

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-data-works.html" />
}}

矢量地图元件仅包含地理/几何图形和它们的元数据，没有任何样式属性。左侧地图是 **Mapbox Terrain tileset** 中的几何图形；右侧地图显示了 **Mapbox Outdoors style** ，它将 `Mapbox Terrain` 和 `Mapbox Streets` 地图元件中的数据结合，并运用特定样式规则制作成现在你在浏览器上所见的这幅地图。更多地图样式运用信息请参考[Map design guide](/help/how-mapbox-works/map-design/) 。

我们所有的地图样式模板都是我们不同地图元件的某种组合运用：

- **Mapbox Streets** 包括基于 [OpenStreetMap](http://www.openstreetmap.org/) 的街道、建筑物、区域、水域以及土地数据。
- **Mapbox Terrain** 包括含有等高线、山影和地表数据的全球高程数据集。
- **Mapbox Traffic** 提供持续的每5分钟更新一次的拥堵信息，这些信息加载在源于OpenStreetMap的道路几何图形上。
- **Mapbox Satellite** 包括由Mapbox处理、拼接的多个来源 [a range of sources](https://www.mapbox.com/about/maps) 的全球卫星影像。更多卫星影像信息请参考卫星影像指南 [Satellite imagery guide](/help/how-mapbox-works/satellite-imagery)。

你也可以在Mapbox Studio中创建自己的地图元件 [create your own tilesets](/help/how-mapbox-works/uploading-data/) 并可以在你的地图中加载你已经在使用的任何Mapbox 地图元件。

## 我们的数据如何工作

这份指南涵盖了Mapbox矢量地图元件的相关信息，它是在你使用Mapbox工具时所接触到的Mapbox提供数据的主要来源。更多关于栅格地图元件的信息请参考 [Satellite imagery guide](/help/how-mapbox-works/satellite-imagery).

### 矢量地图元件

使用矢量地图元件为动态地图的制作提供了附加的功能，包括：

- **动态制作样式**.运用安卓与iOS系统下的 Mapbox GL JS 或 Mapbox Maps SDK，你可以动态地调整你的地图外观，而不需要下载新的图块。
- **流畅的交互**. 因为所有地图数据皆加载在地图用户方，所以你可以快速重新渲染地图，并进行流畅的缩放、倾斜与旋转。
- **尺寸与速度**. 由于矢量图块格式并不固定地拥有小容量或高性能，所以 Mapbox 制图工程师们做了许多工作来确保 Mapbox 所提供的矢量图块在细节与性能之间取得良好平衡。
- **动态查询**. 你可以用这项功能直接从你的矢量地图元件中获取地图的数据属性。

Mapbox 提供三种矢量地图元件，你可以将它们运用到你的地图中。需注意，在某一地图元件中，并非所有数据存在于每个缩放尺度。为使地图尽量精简，Mapbox 制图工程师们仔细选择了各个尺度下应该出现的数据。

请阅读 [Mapbox vector tile specification](https://docs.mapbox.com/vector-tiles/specification/), 每种Mapbox矢量地图元件中的完整图层清单收录在各图层参考中，包括：[Mapbox Streets v8](https://docs.mapbox.com/vector-tiles/reference/mapbox-streets-v8/#layer-reference)， [Mapbox Terrain](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain/#layer-reference)，和 [Mapbox Traffic v1](https://www.mapbox.com/vector-tiles/reference/mapbox-traffic-v1/#layer-reference)。

### 数据源

Mapbox地图元件中的数据来自多个数据源。

#### Mapbox Streets

Mapbox Streets 是一种 Mapbox 提供的包含世界各地的要素如街道、建筑物、地名的地图元件。Mapbox Streets 地图元件是以源自 OpenStreetMap 的开放数据驱动的。 OpenStreetMap 就像是地图的维基百科，它基于开放数据和人人皆可合作制图的理念。任何人都可以快速添加道路及建筑物使得数据跟上现实世界更新的步伐。

Mapbox Streets地图元件在地图要素被编辑或加载时规律更新，这意味着如果你编辑了OpenStreetMap，你最终会看到相应变化体现在Mapbox地图中。想要了解为OpenStreetMap 做贡献的更多信息，请参考 [our OpenStreetMap mapping guides](https://www.mapbox.com/mapping/)。

如需了解有关Mapbox对OpenStreetMap社群贡献的更多信息，请参考 [OpenStreetMap wiki entry on Mapbox](http://wiki.openstreetmap.org/wiki/Mapbox)。

##### 质量保证

<!--copyeditor ignore made-->

除了全球贡献者们的日常努力，OpenStreetMap 社群还运用一些其他方法来发现数据错误，包括多种 [quality-assurance feedback tools](http://wiki.openstreetmap.org/wiki/Quality_assurance) 和一套 [flagging system](http://wiki.openstreetmap.org/wiki/Vandalism)，这套系统允许用户指出疑似错处及需要特别注意的区域。

Mapbox也是OpenStreetMap特别数据小组的大本营。这个小组负责维护地图质量以及添加与优化全世界的地物信息。我们还运用一个自动检测系统来检测出那些疑似编辑错误的地图更新，并将它们提交给我们的数据团队进行人工核查。

#### Mapbox Terrain

Mapbox Terrain是一个Mapbox提供的包含拓扑、山影和地表信息的地图元件。Mapbox Terrain 由广泛数据源组成，包括政府数据集与第三方商业数据。请访问 [mapping platform page](https://www.mapbox.com/about/maps/#data-sources)以了解更多关于Mapbox Terrain地图元件数据集的信息。

#### Mapbox Traffic

Mapbox Traffic是一个Mapbox提供的显示实施交通状况的地图元件。Mapbox Traffic持续自匿名传感器数据中更新与生成信息。Mapbox SDKs收集关于地图与设备位置的匿名数据以持续更新与优化你的地图。请访问 [our telemetry page](https://www.mapbox.com/telemetry/)以了解更多关于Mapbox Traffic地图元件中遥测数据的信息。

### Mapbox Terrain-RGB

**Mapbox Terrain-RGB** 是我们的全球高程图层，它包括以米为单位的原始高度值，以PNG图块中的红、绿、蓝通道呈现。你可以运用Terrain-RGB中的高程数据完成一系列可视化与分析应用，从可视化地形坡度和山影到制作电子游戏中的3D地形。

Terrain-RGB 将每个颜色通道用作一个256进制的计数系统，这样总共会有16,777,216个唯一颜色值。我们以0.1米的高度增量来对应相应的颜色值，这为我们的制图与3D应用提供了必要的垂直精度。

你可以用这个节点来获取Terrain-RGB图块：

```
https://api.mapbox.com/v4/mapbox.terrain-rgb/{z}/{x}/{y}.pngraw?access_token={{ <UserAccessToken /> }}
```

然后用以下公式来将像素值解码为高度值：

```
height = -10000 + ((R * 256 * 256 + G * 256 + B) * 0.1)
```

更多信息请参考我们的 [Access elevation data](/help/troubleshooting/access-elevation-data/) 困难解决指南。

### Mapbox 地图投影

Mapbox支持最受欢迎的 [Web Mercator](http://docs.openlayers.org/library/spherical_mercator.html) 投影，而不支持其他投影。Web Mercator 接近于等角投影，它广泛使用于绝大部分网页地图，因此Mapbox地图与其他使用相同投影的图层能被很好地结合使用。

通常这个投影会被编码成 `EPSG:900913` 或者 `EPSG:3857`。 参见 [epsg.io for more information and alternative encodings](http://epsg.io/3857)。

## 使用我们的数据

你可以将我们的地图数据用作你在Mapbox Studio中地图样式的来源，也可以直接用Mapbox Maps Service APIs 获取数据，或者通过OpenStreetMap来对我们的数据源做贡献。

### Mapbox Studio

你可以直接在Mapbox Studio中的 [Tilesets page](https://www.mapbox.com/studio/tilesets)使用我们的地图元件。当你从Mapbox Studio样式编辑器的模板样式来创建新样式时，即会使用Mapbox地图元件。

### Mapbox Maps Service APIs

通过使用 [Mapbox Maps Service APIs](https://docs.mapbox.com/api/maps/)，你可以以编程方式获取Mapbox地图元件相关信息：

- 使用 **Vector Tiles API** 寻溯矢量图块 [Retrieve vector tiles](https://docs.mapbox.com/api/maps/#vector-tiles) 
- 使用 **Tilequery API** 寻溯矢量图块要素 [Retrieve features from vector tiles](https://docs.mapbox.com/api/maps/#retrieve-features-from-vector-tiles)
- 使用 **Tilesets API** 寻溯TileJSON元数据 [Retrieve TileJSON metadata](https://docs.mapbox.com/api/maps/#retrieve-tilejson-metadata) 

### 为 OpenStreetMap 做贡献

我们为 OpenStreetMap 做贡献，你也应该一起贡献力量！

[Sign up for a free account](https://www.openstreetmap.org/user/new) 免费注册一个账号开始贡献吧。在 OpenStreetMap 网页编辑器中你可以绘制或编辑地物，如道路、建筑物、公园、交通信号灯以及标记。请参考 [Learn OpenStreetMap](http://learnosm.org/en/) 中详细的分步骤指南开始加入项目吧。 

以上我们涵盖了 Mapbox 如何运用 OpenStreetMap 数据，数据运用后的质量控制，以及你如何参与这项日益宏大的行动，为每个人提供免费且开放的数据集。
