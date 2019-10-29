---
title: 在ArcGIS Online中添加Mapbox Studio样式作为底图
description: 将地图添加为ArcGIS Online的底图.
thumbnail: arcgisOnline
level: 2
topics:
- third party integration
language:
- No code
prereq: Familiarity with and access to ArcGIS Online.
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

Mapbox允许你将[Mapbox工作室样式](https://www.mapbox.com/studio/styles)整合入[ArcGIS Online](https://www.arcgis.com/home)中。在这篇教程中，您将学习到如何将Mapbox账号中的样式作为切片图层添加至ArcGIS Online中。

## 操作准备

在按教程操作前您需要作如下准备：

- **ArcGIS Online 账号**。 您可以在[ArcGIS网站](https://www.arcgis.com/home/createaccount.html)上注册免费帐户。
- **集成 URL**。 您可以在*Share &amp; use* 窗口中找到[地图样式](https://www.mapbox.com/studio)的集成URL。我们将在后续步骤中详细介绍如何找到。
## 在ArcGIS中创建一个新项目

找到您的ArcGIS Online项目页面并创建一个新的项目：

- 登录ArcGIS Online。
- 找到[**制图**](http://www.arcgisonline.cn/arcgis/home/index.html)页面。网页将自动为您生成一个新项目。
- 点击 **添加** > **从Web添加图层**。

{{
  <AppropriateImage
    imageId="arcgisDropdown"
    alt="how to initialize adding a layer from web in ArcGIS"
  />
}}

从打开的新窗口中的下拉菜单里选择**切片图层**。

{{
  <AppropriateImage
    imageId="arcgisTileLayerBlank"
    alt="how to specify a tile layer in ArcGIS"
  />
}}

## 查找您的ArcGIS集成URL

在浏览器中新开一个选项卡，打开Mapbox工作室并找到您的ArcGIS集成URL：

- 登录 [Mapbox工作室](https://www.mapbox.com/studio)。
- 在样式编辑器中打开您准备使用的样式。
- 点击顶部菜单栏中的 **Share...** 按钮。
- 在 **Share**窗口打开后，请确认正在查看的是**Production** 选项卡。
- 切换到**Third party** 选项。
- 在下拉列表中选择 **ArcGIS Online** 选项。
- 点击剪贴板图标{{<Icon name='menu' inline={true} />}}复制URL。

{{
  <AppropriateImage
    imageId="arcgisSharePage"
    alt="Screenshot showing the Share modal in Mapbox Studio"
  />
}}

## 将Mapbox样式添加为切片图层

返回ArcGIS Online完成切片图层添加

<!--copyeditor ignore basemap-->

- 回到您的ArcGIS Online项目中。
- 在之前步骤中打开的**从Web添加图层**的窗口里，将您的ArcGIS集成URL粘贴至**URL** 栏中。
- 勾选用作底图 **用作底图**选项。
- 在**标题栏**中输入图层标题。
- 添加 "© OpenStreetMap contributors Design © Mapbox" 至 **制作者名单**。
- 点击 **添加图层**.

{{
  <AppropriateImage
    imageId="arcgisTileLayerFilled"
    alt="complete add layer from web form in ArcGIS"
  />
}}

## 完成项目

您已成功将Mapbox工作室样式添加至ArcGIS Online项目中！

<iframe width="500" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Mapbox and Esri" src="//www.arcgis.com/apps/Embed/index.html?webmap=9584661e8d7341bc8a6708defb704419&extent=-123.4323,45.1638,-121.8598,45.8605&zoom=true&previewImage=false&scale=true&disable_scroll=true&theme=light"></iframe>

## 后续步骤

如果您对在ArcGIS Online中使用在Mapbox工作室中创建的自定义或品牌风格样式感兴趣，请查看我们的[创建自定义样式](/help/tutorials/create-a-custom-style) 教程。
