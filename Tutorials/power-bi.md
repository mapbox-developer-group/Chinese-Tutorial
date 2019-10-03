---
title: Create data visualizations with the Mapbox Visual for Power BI
description: Use Microsoft Power BI to create a custom data visualization.
thumbnail: powerBi
level: 2
topics:
- third party integration
language:
- No code
prereq: Familiarity with Microsoft Power BI.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

通过使用微软Power BI桌面版以及在线版所提供的Mapbox Visual工具，制作可定制化的热力图、点状聚类图以及可变尺寸圆圈统计图。

Mapbox Visual可以在Power BI程序中作为一个可视化插件使用。此教程将会展示Mapbox Visual的一些初级使用技巧以及如何使用[微软Power BI](https://powerbi.microsoft.com/en-us/)来创建一个Mapbox驱动的可视化实例。此教程要求您已经拥有一个Mapbox的账号以及一个微软Power BI的账号。

![an interactive data visualization on a map](/help/img/3rdparty/power-bi-final-product.gif)

## 准备工作

您需要进行以下准备工作：

- **Mapbox账号**：如果要将Mapbox Visual工具添加到Power BI程序中，您将需要一个Mapbox秘钥。此秘钥可以通过[免费注册](https://account.mapbox.com/auth/signup/)获取。
- **Power BI账号**：登陆您的[Power BI账号](https://app.powerbi.com/)或者创建一个新的账号。
- **支持微软Power BI的Mapbox Visual插件**：您可以在Power BI应用中心找到并添加Mapbox Visual，或者您也可以从[Github](https://github.com/mapbox/mapboxgl-powerbi)下载[Mapbox Visual最新版本](https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz)。详情请阅读本教程。
- **数据**：本教程使用的数据来自于[美国的人寿保险开销的统计数据](https://catalog.data.gov/dataset/)。

{{
<Button href="/help/data/power-bi-healthcare-spending.csv" passthroughProps={{ download: "power-bi-healthcare-spending" }} >
    <Icon name='arrow-down' inline={true} /> 点击下载数据
</Button>
}}


## 向Power BI中添加数据

我们首先介绍如何向Power BI工作环境中添加数据。

{{<Note imageComponent={<BookImage />}>}}

这部分教程将展示如果在Power BI在线版本中使用Mapbox Visual。桌面版的操作流程基本一致，但是界面有所差别。

{{</Note>}}


### 添加一个新的数据集

1. 登陆您的Power BI账号。
2. 点击**获取数据**以载入或者连接数据集。
3. 选择_载入一个文件_以载入您之前已经准备好的数据集。
4. 选择_本地文件_以上传本地的CSV格式的文件。

{{<Note imageComponent={<BookImage />}>}}

您可以在_微软Power BI中的Mapbox Visual_使用包含地理坐标信息的任何数据。

{{</Note>}}

![add a new data file to your Power BI account](/help/img/3rdparty/power-bi-add-data.png)

### 创建一个新的报告

在您的Power BI工作环境中，点击**数据集**标签，然后点击柱状图图标以创建一个新的报告。报告结果窗口会自动弹出，您将可以在这个窗口中修改报告。

![create a new report in your Power BI workspace](/help/img/3rdparty/power-bi-create-workspace.gif)

### 将Mapbox Visual添加到您的报告中

您需要通过使用_可视化_窗格来添加Mapbox Visual工具。

1. 在_可视化_窗格中，点击选项**载入自定义可视化**。选项图标由三个小点构成。
2. 选择**从应用商店导入**。
3. 在搜索栏中输入“Mapbox”并回车。
4. 点击位于_Mapbox Visual_选项旁边的**添加**按钮以将其添加至您的Power BI报告中。成功添加后，Mapbox的蓝色图标会显示在_可视化_工具栏中。

{{<img alt='Screenshot showing the Mapbox Visual icon in the Visualizations pane in Power BI' src='/help/img/3rdparty/power-bi-choropleth-mapbox-visual.png' className='block wmax600 mx-auto' />}}

{{<Note title='Alternative workflow: Manual upload' imageComponent={<BookImage />}>}}

或者你也可以从[Mapbox](https://github.com/mapbox/mapboxgl-powerbi)下载[最新版本的Mpabox Visual](https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz):

1. 点击**添加一个自定义可视化插件**按钮并选择**从文件导入**。
2. 上传[最新版本的Mapbox Visual文件](https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz)。
3. 一个蓝色的图标会在添加成功后显示在_可视化_窗格中。

{{</Note>}}

## 创建一个可视化

点击_可视化_窗格中的Mapbox图标以在您的报告中添加一个新的可视化。在自定义您的可视化过程中，您将会同时使用_可视化_窗格中的_字段_和_格式_窗格：

- _字段_窗格能够将数据字段和不同的Mapbox图层（例如热力图、圆圈统计图、聚类图）相互连接。
- _格式_窗格可以用于定义每一个图层的可视化风格，例如颜色和半径范围。

### 初始化一个可视化

在_字段_窗格中，将数据中`latitude`和`longitude`字段分别拖拽至_Latitude_以及_Longitude_栏目中。请务必将两个字段的_无需总结_选项选中。Mapbox可视化容器会自动弹出指令以帮助您完成您的第一个可视化。

通过秘钥连接您的Mapbox账号：

1. 在可视化容器中点击链接，**点击此处以获取免费Mapbox秘钥**。如有提示，请允许访问外部链接。您将会被转接到Mapbox登录界面。
2. 如果您没有Mapbox账号，您可以使用你的邮箱注册新的账号。
3. 在[账户页面](https://www.mapbox.com/account/access-tokens)复制您的Mapbox秘钥。
4. 返回到Power BI，在_格式_窗格中找到_可视化设置_选项并在_秘钥_一栏中粘贴您的秘钥。

![animated GIF illustrating the process outlined above](/help/img/3rdparty/power-bi-initiate-viz.gif)

您将会看到你的第一个地图可视化！

![the resulting data visualization: a map with uniform circles at every point from the dataset](/help/img/3rdparty/power-bi-first-visualization.png)


### 修改地图风格

您可以利用Power BI中的Mapbox Visual来修改可视化中的地图风格。您可以使用任何Mapbox的默认设置，也可以在Mapbox Studio中自定义新风格。如果需要更新您的地图风格，您需要：

1. 在_字段_窗格中，选择_可视化设置_ > _地图风格_。
2. 选择任何一个默认的地图风格。此教程使用Mapbox卫星图风格。

{{<Note title='Custom map styles' imageComponent={<BookImage />}>}}

在**自定义风格**中，您可以从您的Mapbox Studio账户中选择任何一个您的自定义地图风格。这一项功能对于添加自定义多边形和无人机影像，或者对于Mapbox可视化内容以及设计格式的微调都非常重要，它能够更好的帮助您突出您的设计意图及宗旨。

当您使用**自定义风格**的时候，系统会提示您添加一个_风格链接_。请访问[此链接](/help/glossary/style-url)以获取更多的关于自定义风格链接的信息。

如果您想要学习更多的关于在Mapbox Studio中创建自定义地图风格的知识，请阅读[Mapbox Studio使用手册](https://docs.mapbox.com/studio-manual/)或者这篇[关于创建自定义地图风格的教程](/help/tutorials/create-a-custom-style)。如果您有任何问题，请联系[Mapbox客服](https://www.mapbox.com/contact/support)。

{{</Note>}}

现在，您的数据已经叠加在了卫星图层上。

![the same data visualization as above, but with a satellite map behind the circle layer](/help/img/3rdparty/power-bi-viz-settings-map-style.png)

## 创建一个聚类图层

接下来，您将通过调节可视化参数以及使用一个聚类图来展示美国平均人寿保险支出最低的区域。

在_字段_窗格中，在您的数据把`平均保险费用`字段添加到_聚类_栏目中。

在_格式_窗格中：

1. 显示_聚类_图层，隐层_圆圈_图层。
2. 在_聚类_中，从_聚类算法类型_下拉菜单中选择`最大值`。

### 修改聚类可视化的风格

在_格式_窗格中：

1. 将_最小颜色值_修改为`FEC0BF`，将_最大颜色值_修改为`FF0027`。
2. 将_聚类半径_修改为`30`。
3. 将_模糊值_修改为`0`。
4. 将_笔画粗细_修改为`3`。
5. 将_最大放大倍数_修改为`6`。

![screenshot of the Power BI UI with the properties as specified above](/help/img/3rdparty/power-bi-cluster-styled.png)


## 根据缩放度更新图层

如果您想要在不同的缩放程度下显示不同的数据，您可以通过Power BI的Mapbox Visual，在同一个可视化中使用多个图层。您需要给每一个缩放度设置一个对应的显示图层。接下来这个例子展示了如何设置在缩小图层的时候显示一个聚类图，在放大图层的时候显示一个圆圈统计图。

### 将数据属性添加至栏目

在_字段_窗格中：

1. 给`平均保险费用`添加_颜色_和_尺寸_栏目。
2. 将`提供人ID`添加到_提示_栏目中。

![screenshot of the Power BI UI with the properties as specified above](/help/img/3rdparty/power-bi-add-shelves.png)

### 修改圆圈的风格

在_格式_窗格中将_圆圈_图层重新设置为**显示**，并更新风格属性：

1. 将圆圈的_半径_设置为`1`，将_缩放尺度_设置为`10`。
2. 将圆圈的_最小颜色值_设置为`FEC0BF`，_中等颜色值_设置为`FD817E`，以及_最大颜色值_设置为`FF0027`。
3. 将圆圈的_笔画颜色_设置为白色。
4. 将圆圈的_最小缩放度_设置为`6`。当聚类图层显示的时候，圆圈统计图图层会隐藏。

![screenshot of the Power BI UI with the properties as specified above](/help/img/3rdparty/power-bi-update-on-zoom.png)

## 最终结果图

您已经成功使用微软Power BI中的Mapbox Visual工具制作一份可视化报告。

![an interactive data visualization on a map](/help/img/3rdparty/power-bi-final-product.gif)


## 下一步

您可以在[Github](https://github.com/mapbox/mapboxgl-powerbi)或者[客服处](https://www.mapbox.com/contact/support/#other)寻求更多的帮助或者排查疑难杂症的经验。

想要更加深入的学习Mapbox和Power BI吗？[在这里](https://www.mapbox.com/contact/sales)您可以了解到更多的可能性，包括通过添加自定义的shapefile文件来可视化领土范围、添加详细的室内地图，或者是大型点集数据的可视化。
