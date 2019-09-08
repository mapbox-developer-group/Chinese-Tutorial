---
title: Add a Mapbox style to a CARTO map
description: Add your map as a basemap to CARTO.
thumbnail: carto
level: 1
topics:
- third party integration
language:
- No code
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: tutorial
---

<!--copyeditor disable basemap-->

通过[Mapbox工作室](https://www.mapbox.com/studio) 中的样式编辑器或[工作室经典](https://github.com/mapbox/mapbox-studio-classic)创建的地图样式可以作为底图添加至CARTO平台。您可以将任何预先在Mapbox中设置的底图或自定义样式添加为CARTO地图的基本底图。
## 操作准备

在这个教程中，您需要有一个Mapbox账号和一个CARTO账号。请分别登录两个账号，然后继续下一步操作。

打开您准备添加Mapbox样式的CARTO项目。点击左侧的铅笔图标然后点击列表中出现的的当前**底图**。

<img alt='CARTO change basemap dialog' src='/help/img/3rdparty/cartodb-change-basemap.png' class='block wmax600 mx-auto'>

在_Style_选项栏中，点击+。
<img alt='Add a style in CARTO' src='/help/img/3rdparty/cartodb-add-style.png' class='block wmax600 mx-auto'>

## 添加在Mapbox工作室创建的地图样式

在Mapbox工作室中，点击您想要添加到CARTO项目的地图样式旁的**Share &amp; use** 按钮。

![Mapbox style share and use modal](/help/img/3rdparty/cartodb-style-share.png)

在**Share &amp; use** 窗口打开后，切换到**Use**选项卡，然后点击**Third party**选项并切换到**CARTO**。点击剪贴板图标{{<Icon name='clipboard' inline={true} />}} 复制共享地址URL。

<img alt='Mapbox style Use modal CARTO item' src='/help/img/3rdparty/cartodb-share-page.png' class='block mx-auto'>

回到CARTO平台中，将您在上一步操作中复制的共享地址URL粘贴到文本框中，然后点击**ADD BASEMAP**。

![CARTO add basemap dialog](/help/img/3rdparty/cartodb-add-studio-xyz.png)

您希望添加的Mapbox工作室样式将会作为CARTO底图显示。

## 添加使用工作室经典创建的地图样式

在Mapbox工作室中访问[mapbox.com/studio/classic](https://www.mapbox.com/studio/classic)的工作室经典界面。找到您希望使用的样式，然后点击剪切板图标{{<Icon name='clipboard' inline={true} />}}复制样式的图块集ID。

返回到您的CARTO项目中，找到刚刚打开的“更改底图”对话框并点击 **Mapbox** 选项卡。将您在上一步中复制的图块集ID粘贴到“输入您的地图ID/URL”文本框中。您还需要将一个有效的[access token](https://www.mapbox.com/account/access-tokens) 粘贴到“输入访问令牌”文本框中。点击**ADD BASEMAP**以完成Mapbox底图添加。
![CARTO add Mapbox map dialog](/help/img/3rdparty/cartodb-add-classic.png)

您希望添加的Mapbox工作室经典样式将会作为CARTO底图显示。

## 完成工作

您已成功将Mapbox工作室和Mapbox工作室经典中的样式添加至CARTO底图中！
