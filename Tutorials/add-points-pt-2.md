---
title: "Add points to a web map, part 2: create a style"
description: Add a tileset to a template style and upload custom icons in Mapbox Studio.
thumbnail: addPointsPt2
level: 1
topics:
- uploads
- map design
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
  - "import { Video } from '../../components/video';"
  - "import Publish from '../../video/add-points-pt-2-publish.mp4';"
contentType: tutorial
---

这是 [series of tutorials](https://docs.mapbox.com/studio-manual/help/#add-points-to-a-map) 中的第二部分，在这一部分中将会教您如何使用 Mapbox Studio 数据集编辑器、 Mapbox Studio 样式编辑器和 Mapbox GL JS 在网络地图中添加点。
*第二部分* Mapbox Studio 关注于样式编辑器。在本教程中，您将会学习如何：

- 利用 Mapbox 默认样式创建一个新的样式
- 添加一个地形数据集作为图层
- 设置新图层样式
- 发布样式

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjgiiz9ck002j2ss5zur1vjji.html?access_token=MapboxAccessToken#10.7/41.893748/-87.661557/0" />
}}

## 准备

以下是在使用教程中将会用到的一些资源：

- **地形数据集。** 您将需要一个包含10个芝加哥公园的地形数据集。您可以在 [Add points to a web map, Part 1: create a dataset](/help/tutorials/add-points-pt-1) 中学习如何创建这个地形数据集。
- **自定义图标。** 本教程使用自定义图标显示公园的位置。 您需要下载 SVG 图标才能在您的样式中使用。

{{
<Button href="/help/data/marker-editor.svg" passthroughProps={{ download: "marker-editor" }} >
    <Icon name='arrow-down' inline={true} /> Download SVG icon
</Button>
}}

## 将数据添加到一个样式中

Web地图由 [map tiles](/help/how-mapbox-works/web-apps/) 组成。要将数据添加到Web地图， Mapbox 会将其切割为切片，以便数据以各种缩放级别显示。 Mapbox 将地图切割成的图块集合称为切片集。在 [Add points to a web map, part 1: create a dataset](/help/tutorials/add-points-pt-1) 时，您将数据集转换为地图切片集以将其添加到新的地图样式。

### 创建一个新样式

在完成 [Add points to a web map, part 1: create a dataset](/help/tutorials/add-points-pt-1) 后，利用基础模板创建一个新的样式。在 Mapbox Studio 的[Styles page](https://studio.mapbox.com/styles) 上，单击 **New style** 按钮。找到 _Basic Template_ 样式，然后单击 **Customize Basic Template** 。

样式编辑器会自动打开。使用屏幕左上角的标题字段将新样式重命名为 _Chicago Parks_ 。

{{
  <AppropriateImage
    imageId="addPointsPt2RenameStyle"
    alt="Mapbox Studio style editor showing how to rename a style"
  />
}}

### 创建一个新的图层

您将会添加您的地图切片集作为一个新的图层：

1. 当样式编辑器打开时，点击左上方的 **+Add layer** 。
2. 在 _Data sources_ 中，找到您的 **chicago-parks** 地形数据集，点击数据集的名字，然后点击显示的源图层，将其添加为图层的源。

{{
  <AppropriateImage
    imageId="addPointsPt2AddLayer"
    alt="screenshot illustrating how to add a new layer in Mapbox Studio"
  />
}}

3. Mapbox Studio 可识别您上传的数据集中在不同的位置，因此会显示消息 _“此地图视图中无法使用此切片集”_ 。点击 **Go to data** ，地图视图将重新聚焦芝加哥。
4. 点击 **Type** 选项，然后选择 _Symbol_ 图层选项，以便创建带有[markers](/help/glossary/marker/) 的图层。
5. 点击返回 **Style** 选项卡。 

{{
  <AppropriateImage
    imageId="addPointsPt2CreateLayer"
    alt="screenshot illustrating how to create a new layer in Mapbox Studio"
  />
}}

## 图层样式

在 Mapbox Studio 样式编辑器中，您可以指定每个图层的样式属性。这包括 Mapbox 默认样式中的图层以及您使用自定义数据添加的任何图层。对于此示例，您将设置 *symbol* 图层的样式。您可以使用文本和图标设置符号图层样式。

### 将样式作为一个符号图层

1. 点击在样式编辑器左侧的图层列表中创建的 **芝加哥公园** 图层。
2. 样式面板打开后，如果您创建的图层尚未存在，请单击 **Style** 选项卡。
3. 选择 **Icon** 选项卡，然后点击 **Manage icons in your spritesheet** 。
4. 这将打开顶部工具栏的 **Images** 设置。

{{
  <AppropriateImage
    imageId="addPointsPt2UploadSvg"
    alt="screenshot demonstrating the upload SVG menu in Mapbox studio"
  />
}}

5. 点击 **Upload SVG Image** 按钮，从文件中选择您在本教程开头下载的标记。
6. 图标下载完成后，在列表中选择它。

{{
  <AppropriateImage
    imageId="addPointsPt2SelectIcon"
    alt="screenshot demonstrating the upload SVG menu in Mapbox studio"
  />
}}

7. 如果您想显示所有标记，即使它们有所重叠，也请单击 **Placement** 选项卡。向下滚动到 **Allow icon overlap** 并将其设置为`True`。

您现在应该会在所有点上看到标志。

{{
  <AppropriateImage
    imageId="addPointsPt2IconsLoaded"
    alt="screenshot showing a style with a custom icon loaded in Mapbox Studio"
  />
}}

## 发布样式

现在您已经完成了地图的样式设置，您需要发布您的样式以使这些更改在Web上生效。

1. 单击编辑器右上角的 **Pubilsh** 按钮。
2. 弹出一个窗口，要求您查看更改。
3. 点击 **Publish** 。

{{
  <Video
    filename={Publish}
    title="Comparing styles in the Publish modal"
  />
}}

## 共享

[Share modal](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) 包括在Web应用程序，移动应用程序或其他第三方工具中发布样式所需的资源。

### 共享

单击样式编辑器右上角的 **Share** 。共享模块包含一个共享URL，允许您与其他人共享样式预览。该模块还包含样式URL和访问令牌， [part three of this tutorial](/help/tutorials/add-points-pt-3/) 中都需要它们。

{{
  <AppropriateImage
    imageId="addPointsPt2ShareStyle"
    alt="Screenshot showing the share section for a style in Mapbox Studio"
  />
}}

## 下一步

前往 [Add points to a web map, part 3: add interactivity](/help/tutorials/add-points-pt-3/) 并使用 Mapbox GL JS 向您的地图添加有关每个公园的信息弹出窗口。
