---
title: Add 3D buildings to a Mapbox Studio style
description: Add a 3D building layer to a map style in Mapbox Studio.
thumbnail: add3dBuildingsStudio
topics:
- map design
level: 1
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { Video } from '../../components/video';"
  - "import ChangePitch from '../../video/add-3d-buildings-studio-change-pitch.mp4';"
contentType: tutorial
---

本教程将指导您使用 Mapbox Studio 向地图样式中添加3D建筑图层。

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjj0b5ie80ec32so5uo8ox21m.html?fresh=true&access_token=MapboxAccessToken#15/40.751589/-73.986485/-28/60" />
}}

## 准备

在开始本教程之前，您需要在 [mapbox.com/account](https://account.mapbox.com) 创建一个 Mapbox 账号。

## 创建一个新样式

首先，您需要在 Mapbox Studio 里创建一个新的地图样式。

1. 登录您的 Mapbox 帐户并导航到 [Styles](https://studio.mapbox.com/styles) 页面。
2. 点击 **New style** 按钮。找到 _the Basic Template_ 样式，然后单击 **Customize Basic Template** 。
3. 在 Mapbox Studio 样式编辑器中，重命名此新样式，以便日后查找。单击屏幕左上角的标题字段，并将标题更改为 _3D buildings_ 。
4. 在右上角的搜索栏中，输入“Empire State Building”并选择第一个结果。

{{
<AppropriateImage 
  imageId="add3dBuildingsStudioLocationSearch"
  alt="Screenshot showing a new map view in Mapbox Studio"
/>
}}

地图视图将会以纽约帝国大厦为中心进行移动。

## 编辑建筑物图层

接下来，您将会编辑样式中的建筑物图层。
<!--copyeditor ignore okay-->
1. 在屏幕左侧的图层面板中，选择 **building** 图层。
2. 点击 **Select data** 。它可以打开X射线视图，显示来自建筑层的数据。
3. 单击 _New layer_ 面板中的 **Type** 选项，然后选择 _Fill extrusion_ 选项。如果系统提示您这样做，请单击 **Okay** 以确认更改图层类型。
4. 移除此层上显示的所有过滤器。
5. 单击 **+ Create filter** 并选择 **extrude** 数据属性。
6. 将下拉菜单设置为任意，然后单击 **Empty** 按钮。
7. 选择 **true** 。
8. 点击 **Style** 选项，返回建筑物图层的样式面板。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioEditFilter"
    alt="Screenshot showing how to edit a layer filter in Mapbox Studio"
  />
}}

现在建筑图层的类型已经更改，还需要调整其样式设置以显示所需的3D效果。

{{ <Note imageComponent={<BookImage />}> }}
本教程利用了 Mapbox Streets v7 中的建筑图层。如果您有想要在地图样式中使用的自定义建筑数据，则可以使用 [Mapbox Studio](https://studio.mapbox.com/tilesets/) 或 [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) 将这些数据作为一个地图切片集上传到 Mapbox 。
{{ </Note> }}

## 调整页面样式设置

接下来，您将会通过调整图层高度和基础高度属性来实现想要的3D效果。

### 设置高度属性

1. 选择 _building_ 图层并点击 **Height** 属性。
2. 选择 **Style across data range** 选项。
3. 在 _Choose a numeric data field_ 面板中，单击 **height** 。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioStyleHeight"
    alt="Screenshot showing the style across data range option in Mapbox Studio"
  />
}}

4. 第一部分是已经设置 _height_ 为`0`和 _Fill height_ 为`0`。保持这些设置不变。
5. 在第二部分，保持 _height_ 设置为`999`，并将 _Fill height_ 选项更改为`999`。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioStyleMaxHeight"
    alt="Screenshot showing the style max height option in Mapbox Studio"
  />
}}

### 设置基础高度属性

图层的基本高度属性也需要调整。这将处理任何的建筑物情况，这些建筑物具有基础高度和使其成为形状不同的独立高度。如果不设置基础高度属性，建筑物将失去一些细微的建筑特征。

1. 选择 _building_ 图层，然后点击 **Base height** 。
2. 选择 **Style across data range** 选项。
3. 在 _Choose a numeric data field_ 面板中，选择 **min_height** 。
4. 第一个部分已经设置为 _height_ 为`0`和 _Fill base height_ 为`0`。保持这些设置不变。
5. 在第二个部分，保持 _height_ 设置为`999`，并将 _Fill base heigh_ 选项更改为`999`。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioFillBaseHeight"
    alt="Screenshot showing how to adjust the base height setting in Mapbox Studio"
  />
}}

### 突出显示图层

由于图层列表中的建筑物图层上方有许多项目，因此这些项目在这个样式中会呈现在建筑物的顶部。要使建筑物更加突出，可以将建筑图层移动到图层列表的顶部并隐藏 POI 标签图层。

1. 在图层列表中，单击 **building** 图层并将其拖到图层列表的顶部。
2. 点击 _poi-labe_ 层以选中它。
3. 单击图层列表顶部的{{<Icon name='noeye' inline={true} />}} **Hide layer** 按钮来隐藏图层。

您可以使用{{<Icon name='noeye' inline={true} />}} **Hide layer** 按钮来隐藏不想在最终地图样式中显示的任何图层。

### 更改建筑颜色

建筑物默认的黑色很难区分细节，因此这种样式将会使用较浅的颜色。

单击 **Color** 字段并将其更改为{{<ColorSwatch color="#778899" />}}。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioChangeColor"
    alt="Screenshot showing how to adjust the layer color in Mapbox Studio"
  />
}}

### 更改相机视角

因为默认地图视图看起来是垂直“向下”的，所以很难看到更改这些设置的效果。因此要调整视角，使3D建筑更容易被看到:

右键单击地图视图并拖动鼠标。移动地图，直到达到所需的视角。

{{
  <Video
    filename={ChangePitch}
    title="Video showing how to change the pitch in Mapbox Studio."
  />
}}

### 调整样式的光照

更改填充拉伸层的光照强度可以突出建筑细节，使得不同的建筑易于区分。

1. 在屏幕右上角的工具栏中，单击 {{<Icon name='sun' inline={true} />}} **Light** 选项卡打开 _Extrusion Lighting_ 面板。
2. 使用 _Intensity_ 滑块将光强更改为`0.75`。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioExtrusionLighting"
    alt="Screenshot showing the extrusion lighting panel in Mapbox Studio"
  />
}}

## 发布样式

完成编辑新地图样式后，您可以发布您的更改。

1. 点击屏幕右上角的 **Publish** 按钮。当您点击发布按钮时，将会有一个窗口显示上一版本和当前版本之间的差异。
2. 如果您对所做的编辑满意，请点击 **Publish** 。您的样式就可以分享到各种工具和应用程序中。单击顶部工具栏中的 **Share** 按钮查看所有选项。

## 完成

您已经完成了用3D建筑图层创建一个新的地图样式。

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjj0b5ie80ec32so5uo8ox21m.html?fresh=true&access_token=MapboxAccessToken#15/40.751589/-73.986485/-28/60" />
}}

## 接下来

有许多可以使用新 Mapbox Studio 样式的方法。您可以在您的网站上、网络或移动应用程序中使用该地图。请查看 Mapbox Studio 手册中的 [Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) ，以了解使用地图样式的更多方法。
