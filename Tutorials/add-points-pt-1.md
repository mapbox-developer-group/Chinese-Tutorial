---
title: "向网页地图添加点，第一部分：创建数据集"
description: Create a new dataset containing points.
thumbnail: addPointsPt1
level: 1
topics:
- uploads
- datasets
- geocoding
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

本教程是[系列教程](https://www.mapbox.com/studio-manual/help/#add-points-to-a-map) 的第一部，它将教会你如何使用Mapbox studio 编辑器，Mapbox Studio style编辑器和Mapbox GLJS在地图上添加点。

*本系列的第一部分*  重点介绍Mapbox Studiodataset编辑器，在教程里，你将会学习到如何：

- 上传地理空间数据作为dataset
- 在数据集编辑器中绘制附加数据
- 作为tileset保存和导出dataset

{{
  <DemoIframe src="/help/demos/add-points-to-a-map/index.html" />
}}

## 开始

以下是一些在指导中需要跟随的资源:

- **Mapbox 账户**. 在[Mapbox](https://account.mapbox.com/auth/signup/)中注册一个免费帐户。
- **数据**.下载下面的GeoJSON 文件，其中包含九个不同芝加哥公园的坐标和功能属性。

{{
<Button href="/help/data/chicago-parks.geojson" passthroughProps={{ download: "chicago-parks.geojson" }}>
    <Icon name='arrow-down' inline={true} /> Download GeoJSON
</Button>
}}

## 上传新的dataset

通过将数据作为dataset上传到Mapbox Studio，您可以在Mapbox帐户中存储数据的可编辑版本。拥有数据的可编辑版本意味着可以为每个特性添加、删除和编辑特性(点、线和多边形)和属性。

{{
<Note
  imageComponent={<BookImage />}
>
  <p>如果您不需要从头开始编辑或绘制数据，您可以将数据作为<em>tileset</em>而不是<em>dataset</em>上传到Mapbox。了解有关tileset和数据集之间的区别的更多信息，请参见Mapbox Studio手册的上传部分。 <a href='https://www.mapbox.com/studio-manual/overview/geospatial-data/'>Uploads section</a> of the <a href='https://www.mapbox.com/studio-manual/'>Mapbox Studio Manual</a>.</p>
</Note>
}}

### 创建一个Datasets

1. 登入 [Mapbox Studio](https://www.mapbox.com/studio) 并导航至[Datasets 页面](https://www.mapbox.com/studio/datasets)。
1. 点击 **New dataset** 按钮。
1. 选择 the _New Dataset_ modal右上角的**Upload** 选项。
1. 选择下载的GeoJSON 文件，点击 **Confirm**,然后点击**Create**。
<img src='/help/img/studio/point-tutorial-dataset-upload.png' alt='Screenshot illustrating how to create a dataset in Mapbox Studio' class='block wmax600 pt18 mx-auto'>
1. 当你的文件上传完成, 点击 **Start editing**. dataset编辑器自动打开, 数据会显示在一个黑色的基础地图上，使得功能可视化。

![显示Mapbox Studio数据集编辑器的屏幕截图](/help/img/studio/point-tutorial-dataset-editor.png)

### 关于 datasets

您可以在datasets编辑器中编辑datasets特性和属性:

- **特性** 是地图上的点、线和多边形。 您可以使用绘图工具添加新功能，通过单击和拖动地图上的功能来编辑功能的位置或形状，或者通过全选+delete键将所有功能一起删除。您还可以单击dataset 编辑器中的每个特性来查看其属性。

- **属性** 可以是字符串、数字或布尔值。在您上传的示例datasets中，每个点都有“标题”和“描述”属性，它们都有一个惟一的文本字符串。您可以在dataset编辑器中编辑属性、添加新属性或删除属性。*确保在dataset编辑器中工作时，想要在最终产品的弹出窗口中显示的所有内容都包含在属性中。* 

## 绘制数据

可以使用dataset编辑器中的绘图工具向dataset添加新点。也可以使用数据集编辑器的绘图工具更改现有特性的几何形状、位置和属性。有关绘图工具的更多信息，请参阅[Mapbox Studio手册](https://www.mapbox.com/studio-manual/).

### 绘制新特性

1.单击编辑器右上角的**Search places**字段，搜索`Garfield Park Chicago`。 
1. 使用 {{<Icon name='marker' inline={true} />}} 绘图工具 在该位置的地图上创建一个新点。
1. 接下来, 点击 **Add Property** 按钮。使用屏幕左侧的属性列表添加以下域名和描述:
  - 添加域名 `title`并赋值为`Garfield Park`。点击**Confirm**。
  - 添加域名 `description` 并赋值为 `Home of the Garfield Park Conservatory`.点击 **Confirm**.

![animated GIF illustrating how to draw a new feature](/help/img/studio/point-tutorial-dataset-edit.gif)

## 将dataset导出为tileset

接下来，你要将数据集保存并导出为tileset，以便将其添加到Mapbox样式中。


### Create a tileset

1. 单击编辑器右上角的**Save**保存更改。
1. 单击**Export** ，然后选择 _导出为新 tileset_.
1. 命名您的tileset `chicago-parks`并单击 **Export**.
<img src='/help/img/studio/point-tutorial-export-to-tileset.png' alt='Screenshot illustrating how to export a dataset to a tileset in Mapbox Studio' class='block wmax600 pt18 mx-auto'>
1.在您的tileset成功上传之后，单击 _Notifications_窗格中tileset的名称打开它。

<img src='/help/img/studio/point-tutorial-tileset-upload.png' alt='Screenshot illustrating a successful tileset upload in Mapbox Studio' class='block wmax600 mx-auto'>

### 关于tileset

Web地图由 [地图块](/help/how-mapbox-works/web-apps/)组成。一组tile称为tileset。Mapbox将数据分割成小块，然后将这些小块添加到web地图中，并以不同的缩放级别显示。为了使Mapbox的地图性能更优异，数据集的特性在转换为tileset时得到了简化。

## 下一步

接下来，开始本教程系列的[第2部分](/help/tutorials/add-points-pt-2/)，学习如何在Mapbox Studio样式编辑器中将tileset添加到地图样式中。
