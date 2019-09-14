---
title: Style a single country
description: Find and upload open source data to style in Mapbox Studio.
thumbnail: styleSingleCountry
level: 1
topics:
- uploads
- map design
language:
- No code
contentType: tutorial
prependJs:
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import { Video } from '../../components/video';"
  - "import StyleCreate from '../../video/style-single-country-style-create.mp4';"
---

<style>
    .color-swatch {
      width: 15px;
      height: 15px;
      border-radius: 15px;
      display: inline-block;
      margin-bottom: -2px;
    }
</style>

在 [Mapbox Studio](https://studio.mapbox.com) 样式编辑器的帮助下，您可以定制一个国家或地区的样式。在这个例子中，您将定义澳大利亚的样式。

## 开始

在开始之前，您需要注意以下几点事项：

- **Mapbox account** 。您需要一个帐号用来登录和使用 Mapbox Studio 样式编辑器。你可以在 [mapbox.com/account](https://account.mapbox.com) 创建这样的帐号。
- **Natural Earth data** 。 您需要从 [Natural Earth](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/) 下载 `Admin 0 - Countries` 的 Shapefile 文件。

## 创建一个新的样式

登录您的 Mapbox 帐号并跳转到 [Styles](https://studio.mapbox.com/styles) 页面， 那里会列出您的所有地图样式。一个 [style](/help/glossary/style/) 是一组规则，它定义了 Mapbox 在页面上如何绘制您的地图，它包括了您的数据、地图图像（图标、标记和模式）、字体的引用，并且定义了您所有数据在地图上的样式。更多关于样式的信息，请阅读 Mapbox Studio 手册的 [Styles](https://docs.mapbox.com/studio-manual/reference/styles/) 部分。

从您的 [Styles](https://studio.mapbox.com/styles) 页面创建一个新的样式，请点击 **New style** 按钮。向下滑动页面，选择 **Blank** 并点击 **Customize Blank**。这个样式编辑会自动打开。

{{
  <Video
    filename={StyleCreate}
    title="Create a new style modal in Mapbox Studio"
  />
}}

## 使用样式编辑器

使用样式编辑器添加您下载的数据到地图中，并调整国家的样式。

### 添加一个 tileset 源

您可以通过上传的自然地球数据作为一个tileset然后把澳大利亚添加到一个空白的地图画布中：

1. 点击 **+ Layer** 。
2. 在 _Data sources_ 列表中，点击 **+ Upload** 并选择自然地球数据。
3. 右下角将出现一个弹出窗口，显示您上传的进度。
4. 一旦上传 "Succeeded" tileset就可以使用了！
5. 在 _Data sources_ 列表中搜索您的 tileset，并点击这个数据源，然后您就可以使用这个数据源图层了。

您创建的这个 tileset 包含了所有的国家，进行过滤而只使用澳大利亚：

1. 点击 **Filter** 选项，再点击 **+ Create filter** 。
2. 从数据字段中选择 **NAME** 字段。
3. 输入 `Australia` 带搜索框中，再点击 **+ Use Australia** 然后点击 **Done** 。

{{
  <AppropriateImage
    imageId="styleSingleCountryFilter"
    alt="screenshot of how to filter data in the Mapbox Studio style editor"
  />
}}

4. 在原始的面板中，重新选中 **Style** 选项卡。
5. 您将在您的地图画布上看到一个黑边的澳大利亚。

{{
  <AppropriateImage
    imageId="styleSingleCountryNoStyle"
    alt="screenshot of unstyled country"
  />
}}

### 定制数据样式

接下来点击 **Style** 选项卡从而自定义这个图层的外观和感受。改变 **Color** and **1px stroke** 字段为 {{<span className="color-swatch" style={{ backgroundColor: "#11b1f0" }}></span>}} `#11b1f0`。

{{
  <AppropriateImage
    imageId="styleSingleCountryFillColor"
    alt="screenshot of style panel in Mapbox studio"
  />
}}

### Publish

编辑完地图样式后，单击屏幕右上角的 **Publish** 发布更改。当您点击发布按钮时，一个窗口将显示此样式的前一个版本和当前版本之间的差异。如果您对更改感到满意，请单击 **Publish** 。您的样式现在可以在各种工具和应用程序中共享。

## 成品

您已经在外部数据的帮助下的制定了一个国家的样式。Mapbox Studio 提供了多种使用新地图样式的方法。您可以直接在您的网站、web或者移动应用程序中使用此地图。请查阅 Mapbox Studio 手册的 [Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) ，以了解所有使用您的样式的方法！

## 下一步骤

请在 [Mapbox Studio Manual](https://docs.mapbox.com/studio-manual/reference/styles/) 了解更多关于如何使用 Mapbox Studio 样式编辑器的信息。
