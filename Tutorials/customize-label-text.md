---
title: Customize label text for a single label
description: Use expressions in Mapbox Studio to alter a single label.
thumbnail: customizeLabelText
level: 1
topics:
- data
- map design
language:
- No code
contentType: tutorial
prependJs:
  - "import AppropriateImage from '../../components/appropriate-image';"
---

本教程将引导您如何使用 **Mapbox Studio style editor** 中的表达式来自定义单个标签的标签文本。

## 入门指南

在开始之前，您需要注册一个 **Mapbox account** 才能使用 Mapbox Studio 样式编辑器。您可以在 [mapbox.com/account](https://account.mapbox.com) 注册一个账号。

## 创建一个新样式

登录您的 Mapbox 账号并导航到 [Styles page](https://studio.mapbox.com/styles) 。页面里会列出您的所有样式。一种 [style](/help/glossary/style/) 就是 Mapbox 在页面上如何绘制地图的一组规则。它定义了如何设置所有数据的样式，包括对数据、地图图像(图标、标记、图案)和字体的引用。关于样式的更多信息, 请参阅 Mapbox Studio 手册的 [Styles](https://docs.mapbox.com/studio-manual/reference/styles/) 部分。

打开您的 [Styles page](https://studio.mapbox.com) 页面。点击 **New style** 按钮。找到 _Basic Template_ 然后点击 **Customize Basic Template** 。样式编辑器将自动打开基础模板样式以供编辑。

## 使用样式编辑器

**Mapbox Studio style editor** 是一个可根据您的确切要求创建自定义地图样式的可视化工具。请看样式编辑器页面左边的图层。可以用多种方式自定义每图层，包括（但不限于）改变标签。

## 使用表达式编辑图层中的特定标签

单击 **country-label** 图层查看定义此图层样式的所有可设置选项。如需根据数据中的条件和属性自定义国家/地区标签，请点击 **Style with data conditions** 并选择“name_en”以根据国家/地区的英文名称设置标签样式。

{{
  <AppropriateImage
    imageId="customizeLabelText1"
    alt="Mapbox Studio screenshot of 'Style with data conditions'"
  />
}}

在新面板中，系统会提示您填写数据条件的详细信息。 在第一个文本字段中，输入`France`，因为这是您将要自定义的标签。在`Text field`中，添加`"Land in: "`，并输入 **＆** 来组合您的两个字符串。当您这样做时，您会在地图上看到`France`标签更改为`Land in: France`。

{{
  <AppropriateImage
    imageId="customizeLabelText2"
    alt="Mapbox Studio screenshot of data conditions panel"
  />
}}

要编辑其他数据条件，请单击右下角的 **Done** ，然后单击 **Add another condition** 。这次，选择旅程的第一个间隔继续这趟旅程。在第一个文本字段中输入`Spain`，然后在`Text field`输入框中输入`"First stop: "`。


{{
  <AppropriateImage
    imageId="customizeLabelText3"
    alt="Mapbox Studio screenshot of data conditions panel"
  />
}}

重复上一步，在过程中继续添加更多数据条件和间隔点。完成后，您的地图将看起来如下图所示。

{{
  <AppropriateImage
    imageId="customizeLabelText4"
    alt="Mapbox Studio screenshot of completed data conditions"
  />
}}

## 最终产品
您已经使用表达式在地图上更新了特定标签的自定义显示。要想了解有关使用 Mapbox studio样式编辑器的更多信息，请阅读 [Mapbox Studio 手册](https://docs.mapbox.com/studio-manual/) 。

{{
  <AppropriateImage
    imageId="customizeLabelTextFinal"
    alt="final product with customized labels"
  />
}}

