---
title: Create a custom style
description: Alter a template style to create a custom map style.
thumbnail: createACustomStyle
level: 1
topics:
- map design
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { Video } from '../../components/video';"
  - "import BuildingZoom from '../../video/create-a-custom-style-building-zoom.mp4';"
contentType: tutorial
---

本指南将介绍如何在 **Mapbox Studio style editor**中创建一个自定义样式，Mapbox Studio 基本样式是可以定制的，这便于你创建符合你公司品牌的地图样式。
本教程将向您展示如何通过更改颜色、字体和标签属性来定制Mapbox基本样式。在您完成本教程之后，您将完成创建一个地图样式，它可以在世界上任何缩放层级和任何地方反映Mapbox品牌的颜色。

{{
  <DemoIframe src="https://api.mapbox.com/styles/v1/examples/cji3d7gpt1i8m2rn7l7w0vl99.html?access_token=MapboxAccessToken#9.7/37.758664/-122.233084/0" />
}}

## 开始

你需要一些用于开始的资源:

- **Mapbox account**。 在[Mapbox](https://account.mapbox.com/auth/signup/)注册一个免费的账户
- **Style guidelines**。 这些广泛的Style guidelines对于创建一个新的自定义地图样式是非常有帮助的。Mapbox的品牌有三种基色（蓝色，灰色，粉色）和一组更广泛的颜色。每种色调都包括暗、亮、微弱的变化。本教程将使用这些颜色的组合在一个自定义地图样式中为背景、水、建筑物和文字标签着色。

## 创建一个新的样式

使用你的Mapbox帐号登陆并跳转到[Styles](https://studio.mapbox.com/styles)页面，那里会列出你所有的地图样式。一个[style](/help/glossary/style/) 是一组规则，它定义了Mapbox在页面上如何绘制你的地图。它包括了您数据、地图图像（图标、标记和模式）、字体的引用，并且定义了您所有数据在地图上的样式。更多关于样式的信息，请阅读Mapbox Studio手册的[Styles](https://docs.mapbox.com/studio-manual/reference/styles/) 部分。

从您的[Styles](https://studio.mapbox.com/styles)页面创建一个新的样式，请点击**New style**按钮。找到 _Basic Template_ 样式并点击**Customize Basic Template**。

Mapbox Studio 样式编辑器将会打开，您可以开始创建一个自定义地图样式。

## 自定义你的样式

### 样式编辑器

样式编辑器**Mapbox Studio style editor**是一个用于创建自定义地图样式的可视化工具。在样式编辑器界面的左侧您可以看到有一些图层。每一层都可以通过多种方式进行定制，包括更改其颜色。您还可以在图层列表中过滤图层，并同时编辑多个图层的属性。这是改变具有相似属性的图层颜色的最简单的方法。要了解更多关于Mapbox Studio style editor的信息，请访问[Mapbox Studio Manual](https://docs.mapbox.com/studio-manual/reference/styles/)。

在本节中，您将更改水、背景、建筑物图层的颜色，并更改各种标签的字体，以创建自定义地图。

但首先，更改你新样式的名字，点击屏幕左上角的name字段，将名字更改为 _Mapbox Style_.

###  定制背景图层和水图层的样式

当样式编辑器第一次使用基本样式模板打开时，地图已缩放到一个高层级。缩小到大约第10级，这样你可以看到一个更大的地理区域，在搜索栏中，输入Francisco（或者另一个地区，它具有水，陆地，城市特性的良好组合).

{{
  <AppropriateImage
    imageId="createACustomStyleSearchBar"
    alt="Mapbox Studio screenshot showing the map's search bar"
  />
}}

您将从更改水图层和背景图层开始，使它们与Mapbox样式指南中的颜色相匹配。

#### 定制水图层的样式

您将使用Mapbox样式指南中的亮蓝色为**water**图层设置样式。

1. 点击图层列表中的**water**图层。当图层面板打开时，如果它没有高亮显示，点击**Color**字段。
2. 更改颜色为 {{<ColorSwatch color="#314CCD" />}}.

{{
  <AppropriateImage
    imageId="createACustomStyleBackgroundWater"
    alt="Mapbox Studio screenshot showing the water layer panel"
  />
}}


#### 定制背景层的样式

Mapbox Studio允许您根据特定的数据调整样式。在本例中，您将使用样式编辑器根据缩放级别更改样式背景的颜色。使用缩放属性，随着地图的缩放，背景颜色将逐渐变浅。按缩放级别设置背景图层样式：

1. 点击图层列表中的**background**图层。
2. 当图层面板打开时，如果没有高亮显示，点击**Color**选项。
3. 点击**Style across zoom range**.
4. 在 _Zoom_ 面板中，编辑第一个stop，使缩放层级为 `6` 并且颜色为 {{<ColorSwatch color="#A9B6EF" />}}。点击**Done**。
5. 点击第二个stop打开它的 _Zoom_ 面板。将缩放层级改为`12`并且颜色为 {{<ColorSwatch color="#EDF0FD" />}}。点击**Done**。

{{
  <AppropriateImage
    imageId="createACustomStyleBackgroundColor"
    alt="Mapbox studio screenshot showing how to add a color for a specific zoom level"
  />
}}

现在，当您放大地图时，背景颜色会随着缩放层级的增加而逐渐变化。

### 定制土地使用图层和国家公园图层的样式

现在已经更改了水和背景图层的颜色，基本样式中使用的绿色看起来太大胆了。您将把这些层的颜色从样式指南的辅助颜色更改为浅绿色。

1. 选中**national_park**图层.
2. 当图层面板打开时，选择**Color**字段。改变**Color**字段的值为 {{<ColorSwatch color="#E8F5EE" />}}。

{{
  <AppropriateImage
    imageId="createACustomStyleLayerNoDataCondition"
    alt="Mapbox Studio screenshot showing how to change the color for a layer without data conditions"
  />
}}

3. 选中**landuse**图层.
4. 点击**Color**字段如果它没有高亮显示。
5. 点击"`class` is **park, pitch**"条件。
6. 更改**Color**字段为 {{<ColorSwatch color="#E8F5EE" />}}。

{{
  <AppropriateImage
    imageId="createACustomStyleLayerWithDataCondition"
    alt="Mapbox Studio screenshot showing how to change the color for a layer with data conditions"
  />
}}

### 更新字体

接下来，更改样式中用作标签的字体。

1. 点击图层列表顶部的 {{<Icon name='filter' inline={true} />}} **Filter layers** 。
2. 选择**Filter by value**.
3. 选择**Fonts**.
4. 选择`Roboto Black`。这将返回唯一使用字体的图层，**state-label**。
5. 点击**state-label**，然后点击**Font**。更改字体为`Roboto Condensed Bold`。
6. 再次点击{{<Icon name='filter' inline={true} />}} **Filter layers**， 然后对字体`Roboto Regular`重复这个过程，将其更改为`Roboto Medium`。
    - *您可以通过按住* `command` *(Mac) 或者* `CTRL` *(Windows) 同时选择多个图层*

{{
  <AppropriateImage
    imageId="createACustomStyleFontsProp"
    alt="Mapbox Studio screenshot showing how to change font options"
  />
}}

### 定制标签样式

当您更改了字体并设置了一些常规选项之后，就可以更新样式中使用的各种标签类型的颜色了。

<!--copyeditor disable clear-->

1. 点击图层列表顶部的{{<Icon name='filter' inline={true} />}} **Filter layers** 并搜索单词  _label_ 。 这个搜索将返回9个名称中带有单词 _label_ 的图层。
2. 选择 **country-label**。
3. 当图层面板打开时，选择**Color**字段并将其更改为 {{<ColorSwatch color="#ffffff" />}}。
4. 更改**Halo color**字段为 {{<ColorSwatch color="#314CCD" />}}。
5. 更改以下标签层，使其具有以下属性：
  - **place-neighborhood-suburb-label**: `color` {{<ColorSwatch color="#EE4E8B" />}}, `halo color` {{<ColorSwatch color="#ffffff" />}}
  - **place-city-label**: 点击 **Clear value** 并且指定 `color` {{<ColorSwatch color="#ffffff" />}}, `halo color` {{<ColorSwatch color="#273D56" />}}

{{
  <AppropriateImage
    imageId="createACustomStyleFontsPlace"
    alt="Mapbox Studio change style of place labels"
  />
}}

<!--copyeditor enable clear-->

### 定制建筑物样式

接下来，将你的建筑风格的颜色从Mapbox样式指南中更改为一种颜色：

1. 在图层列表中**building**。
2. 当图层面板打开时, 改变**Color**字段为 {{<ColorSwatch color="#aab7ef" />}}.
3. 更改**1px stroke**字段为 {{<ColorSwatch color="#aab7ef" />}}。

{{
  <AppropriateImage
    imageId="createACustomStyleBuildings"
    alt="Mapbox Studio screenshot of how to change building color"
  />
}}

为了确保Mapbox模板样式是高性能的，并不是在每个缩放层级都包含图层。例如，建筑物图层仅在缩放层级为16和更高时可见。当你缩放超过15级时你可以使用缩放功能创建一个淡入效果，而不是当你到达15层级时建筑物突然出现：

1. 在**building**图层的**Opacity**字段中，选择**Style across zoom range**。
2. 点击**Edit**打开并编辑每一个stop：
    - 编辑第一个stop使缩放层级为`15`，opacity `0`. 为了改变透明度， 将不透明度滑块一直向左移动。
    - 编辑第二个stop，使缩放级别为`16`并且opacity为`1`。
3. 放大可以看到建筑物在缩放15到16级之间淡入。

{{
  <Video
    filename={BuildingZoom}
    title="Mapbox Studio video showing building fade effect when zooming"
  />
}}

这种淡入效果也可以应用于道路、公园、水道和您选择的任何其他层。

## 发布

编辑完地图样式后，单击屏幕右上角的**Publish**发布更改。当您点击publish按钮，一个窗口将显示此样式的前一个版本和当前版本之间的差异。如果您对更改感到满意，请单击**Publish**。 您的样式现在可以从各种工具和应用程序中共享。

{{
  <AppropriateImage
    imageId="createACustomStylePublish"
    alt="Mapbox Studio screenshot showing how to publish a style"
  />
}}

## 成品

您已经创建了一个展现Mapbox样式指南的地图，从世界视野到街道水平和世界各地的任何位置。探索您完成的自定义地图样式，并花一些时间在不同的缩放级别查看样式。

{{
  <DemoIframe src="https://api.mapbox.com/styles/v1/examples/cji3d7gpt1i8m2rn7l7w0vl99.html?access_token=MapboxAccessToken#9.7/37.758664/-122.233084/0" />
}}

## 下一步骤

Mapbox Studio 提供了多种使用新地图样式的方法。您可以直接在您的网站或者web或者移动应用程序中使用此地图。查看Mapbox Studio手册的[Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/)，查看所有可以定制样式的方法！
