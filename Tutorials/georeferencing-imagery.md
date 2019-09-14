---
title: 图像的地理配准
description: 在QGIS的帮助下，将非地理参考的航拍图像或历史地图放到Mapbox地图上。
thumbnail: georeferencingImagery
level: 3
topics:
- uploads
- satellite
- third party integration
language:
- No code
prereq: 熟悉QGIS。
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

**地理配准**是将地理坐标分配给栅格图像，并根据地图坐标系统定义其在世界上的位置的过程。 如果您曾经使用过[Mapbox Satellite](/help/glossary/mapbox-satellite/)，那么您已经使用过图像的地理配准。这是因为Mapbox Satellite中的每一个栅格块都是一个被分配到世界上特定位置的图像。

有很多原因可以解释您为什么想要对自己的自定义栅格图像进行地理配准。 例如，您可能会收到非空间图像格式的卫星图像，也可能需要将历史地图与当前地图进行比较，或者您可能正在为游戏应用构建虚构地点的交互式地图。

在本教程中，您将使用[QGIS](http://qgis.org/)对俄勒冈州波特兰市中心的历史JPEG图像进行地理配准，这是一个免费的开源地理信息系统(GIS)。您在QGIS中将图像导出为[GeoTIFF](/help/glossary/tiff/)格式后，并将其作为[tileset](/help/glossary/tileset/)上传到Mapbox帐户。Mapbox不提供内置工具来对图像进行地理配准，因为有免费的开源工具可以执行此操作，例如QGIS。

![historical map of Multnomah county](/help/img/3rdparty/multnomah-county.png)


## 入门指南
在本教程中，您将需要：

- **QGIS**.请按照[下载说明](http://qgis.org/en/site/forusers/download.html)获取更多信息，并确保已安装最新版本。
- **地理配准的图像**.本教程使用JP2(一种高分辨率JPEG)格式的俄勒冈州波特兰市中心的历史地图，您需要下载该地图。这张图片是从[美国国会图书馆](https://www.loc.gov/)提供的[俄勒冈州穆尔特诺玛县的较大的地图](https://www.loc.gov/resource/g4293m.la000694/)上裁剪下来的。{{<sup className='text-sup txt-s'>1</sup>}}

{{
<Button href="/help/data/downtown-pdx.jp2" passthroughProps={{ download: "downtown-pdx" }} >
    <Icon name='arrow-down' inline={true} /> Download image
</Button>
}}

## 在QGIS中对您的图像进行地理配准

首先，您需要按照QGIS的Georeferencing Topo Sheets和Scanned Maps教程中的说明进行操作。 它对地理配准的介绍将指导您使用最新版本的QGIS完成整个过程。 确保使用本教程开头下载的图像，而不是QGIS教程和EPSG：900913或EPSG：3857（Web Mercator）中提供的图像作为坐标参照系（CRS）。

完成您的地理配准后，请确保将GeoTIFF文件保存为**downtown-pdx.tif**，方便您将它上传到Mapbox。

## 以tileset的形式上传到Mapbox

您已成功将JP2图像转换为GeoTIFF，并准备将其作为tileset上传到Mapbox。

您可以在 [Mapbox Studio](https://www.mapbox.com/studio) 中上传GeoTIFF，也可以使用[Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads)以编程方式上传。 有关使用Mapbox Studio上传的详细信息，请阅读[Mapbox Studio手册](https://www.mapbox.com/studio-manual/)的[Uploads](https://www.mapbox.com/studio-manual/overview/geospatial-data/)部分。有关使用Uploads API的更多信息，请阅读[Uploads API 文档](https://docs.mapbox.com/api/maps/#uploads)。

## 最终产物

您对自定义图像进行了地理配准并上传到了您的Mapbox帐户。 现在您可以将您的栅格瓦片格式的图像作为栅格瓦片源添加到任何Mapbox项目中。 这是使用Mapbox GL JS将图像添加到地图的示例。

{{
  <DemoIframe src="/help/demos/georef/index.html" />
}}

## 下一步

要了解有关地理配准的更多信息，请阅读QGIS的高级 [航空图像地理配准](http://www.qgistutorials.com/en/docs/advanced_georeferencing.html) 指南，以提升您的地理配准技能。

---

{{<span className='txt-s'><sup className='text-sup'>1</sup> Habersham，Robert A和Julius Bien＆Co。俄勒冈州摩特诺玛县地图：根据县记录，铁路调查和其他官方数据编制。 [纽约：Julius Bien＆Co Photo。 Lith，1889]地图。 取自美国国会图书馆，https：//www.loc.gov/item/2012586242/。 （2017年4月18日访问。）</span>}}
