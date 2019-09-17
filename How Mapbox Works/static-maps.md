---
title: 静态和印刷地图
description: 学习Mapbox Static Images API 如何工作 以及如何创建静态地图。
image: /img/narrative/print.svg
topics:
  - 印刷
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import { DemoStatic } from '../../components/demo-static';"
contentType: 指引
---

静态地图是独立的PNG格式图片，可以在网页或移动设备上不依赖于地图库或者API进行展示。 它们就像嵌入了一张没有交互和控件的地图。 你可以利用Mapbox静态图片 API ，配合中心点坐标，缩放级别，旋转角度，倾斜角度等参数，请求得到一张静态地图。静态地图也可以包含线、标注或面等覆盖物。 **你可以通过 [静态图片API 演练场](/help/interactive-tools/static-api-playground)学习如何向静态图片API发送一个请求**.

下面这张图片就是通 Mapbox 静态图片 API 生成的，并且可以通过以下代码添加到网页中:

```html
<img alt='static Mapbox map of the San Francisco bay area' src='https://api.mapbox.com/styles/v1/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}/static/-122.337798,37.810550,9.67,0.00,0.00/1000x600@2x?access_token={{ <UserAccessToken /> }}' >
```

{{
  <DemoStatic src="https://api.mapbox.com/styles/v1/mapbox/streets-v{constants.VERSION_STREETS_STYLE}/static/-122.337798,37.810550,9.67,0.00,0.00/1000x600@2x?access_token=MapboxAccessToken" alt="static mapbox map of the san francisco bay area" />
}}


## 静态地图如何工作

Mapbox 静态图片 API 允许你以静态图片的形式请求你Mapbox账户中任何地图样式。 你可以通过几张不同的图片或者几个不同的文件类型生成一张静态地图，这取决于你如何使用Mapbox tool。请参照下文中[如何生成静态地图](/help/how-mapbox-works/static-maps/#creating-static-maps) 以获取API支持的文件类型。

### Retina

当你获取一张 标记有`@2x`的Retina地图时，你将得到一张宽高为API指定宽高2倍的图片。 例如宽度参数设置为700px 并且带有参数 `@2x` 将会收到一个实际参数为1400px的图片。

### 高分辨率图片

Mapbox Studio 允许每个账户使用 [打印面板](https://docs.mapbox.com/studio-manual/reference/styles/#print-panel)输出100张高分辨率图片。如果你想获取更多数量的图片输出请联系 [Mapbox 销售](https://www.mapbox.com/contact/sales)。

使用 Mapbox 静态图片 API， 图片导出尺寸可高达 1,280&nbsp;px x 1,280&nbsp;px 。你能够通过开启retina 以提高图片质量，但是你无法通过使用静态图片 API导出比这更高的分辨率图片了 ，而且我们也不支持导出矢量图片格式。

### 用于印刷的静态图片

想要印刷Mapbox Studio 生产的任何图片，无论有何用途，请 [联系我们](https://www.mapbox.com/contact/sales/). 印刷地图需要 [appropriate Mapbox attribution](/help/how-mapbox-works/attribution#static--print).


## 制作静态地图

以下是各工具支持的生成图片格式列表：

Format | Tool(s)
-------|---------
PNG | [Mapbox静态图片API](https://docs.mapbox.com/api/maps/#static-images)
PNG, JPG<br>high-resolution | [Mapbox Studio](https://www.mapbox.com/studio-manual/reference/styles/#print-panel) (每个账户限制导出数量)

以下格式 **不被支持** 作为地图导出选项 并且也不在我们的整合计划之中：

* SVG
* EPS
* PDF

### Mapbox 静态图片 API

你可以利用一个特定格式的URL请求回去一张静态地图。 详情参考 [静态图片 API 文档](https://docs.mapbox.com/api/maps/#static-images) 以获取可用的参数和值。

### Mapbox 静态图片 API演练场

为了学习如何制作静态图片请求请查看 [Mapbox静态图片API演练场](/help/interactive-tools/static-api-playground).

![screenshot of the Static Images API playground page](/help/img/interactive-tools/static-api-playground.png)

#### 覆盖物

你可以为使用静态图片 API生成的任何地图添覆盖物。 覆盖物是一种能够在请求时添加到地图顶层的数据。覆盖物数据使用逗号分隔，可以混合使用 GeoJSON，自定义 markers， 路径，或面。过于如何在地图上添加覆盖物请阅读[静态图片 API 文档](https://docs.mapbox.com/api/maps/#static-images)。

### Mapbox Studio

Mapbox Studio 打印面板 允许你导出高分辨率自定义地图样式。 点击 {{<Icon name='printer' inline={true} />}} 打印图标以切换打印面板的开关。 在打印面板中可以调整地图位置和 **打印输出设置** 。设置包含图片尺寸 (单位英寸 或 厘米)，分辨率 (单位像素或英寸)，以及文件格式 (PNG 或 JPG). 最大的图片导出尺寸是 8,000&nbsp;px x 8,000&nbsp;px。

关于打印面板的详细信息请阅读 [Mapbox Studio 手册](https://www.mapbox.com/studio-manual/reference/styles/#print-panel).

![screenshot of the print panel with print export settings as described above](/help/img/studio/print-export-settings.png)
