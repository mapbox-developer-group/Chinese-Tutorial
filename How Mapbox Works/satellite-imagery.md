---
title: 卫星影像
description: 学习卫星影像原理以及如何在你的下一个Mapbox项目中使用它。
image: /img/narrative/satellite.svg
topics:
  - 卫星影像
contentType: 指引
---

[Mapbox Satellite](/help/glossary/mapbox-satellite) 是一种全球的高分辨率卫星影像基础地图,  [Mapbox Satellite Streets](https://www.mapbox.com/maps/satellite)则结合了 Mapbox Satellite 基础地图，以及 [Mapbox Streets](https://www.mapbox.com/maps/streets/)的矢量数据为你的地图加入上下文信息。 影像数据来源于多样化的商业数据提供商，当然也包含来自于 NASA，USGS，以及其它机构的开源数据。 它们经过色彩纠正以及混合后被融入一套 raster [tileset](/help/glossary/tileset/). 这是一篇概述卫星影像如何工作以及教你如何在你的项目中使用卫星影像的教程。

![satellite imagery of Cyclone Debbie](/help/img/satellite/cyclone-debbie.jpg)

<div class='caption' markdown='1'>
Imagery of Tropical Cyclone Debbie off the coast of Australia in the spring of 2017.
</div>

## 卫星影像如何工作

我们的卫星影像来自于多样的栅格数据 并通过Mapbox加工混合在一起。

### 栅格数据

所有的卫星影像都被存储为栅格格式。 栅格是一种 [基于像素的数据格式](http://en.wikipedia.org/wiki/Raster_graphics) 它可以高效的表现连续的表面。 栅格的信息基本单元是一种网格结构或者像素， 它们有着相同的尺寸，但是在取值上不同。 数码相片，正射投影和卫星影像都是以这种格式被存储的。

![rasters-are-pixels](/help/img/satellite/rasters-are-pixels.png)

栅格格式 非常适合于分析随时间和空间变化的数据，因为每一个数据值都有一个可获取的基于网格的位置。这就允许我们从两幅或者多幅栅格图中获取同一位置的数据，并进行比较。

### 卫星栅格

当地球观测卫星记录一张图片时， 它们从波长中会读取并记录电磁光谱的反射率。

![diagram of electromagnetic spectrum](/help/img/satellite/rasters-emspectrum.png)

<div class='caption' markdown='1'>
**Source**: Comparison of wavelength, frequency and energy for the electromagnetic spectrum.” Digital image. The Electromagnetic Spectrum. March 2013. Accessed June 2017. [https://imagine.gsfc.nasa.gov/science/toolbox/emspectrum1](https://imagine.gsfc.nasa.gov/science/toolbox/emspectrum1.html).
</div>

<!--copyeditor ignore previously-->
人眼只能看到 [电磁波谱](http://en.wikipedia.org/wiki/Electromagnetic_spectrum)中的很小一部分。 这部分被称作 _可见光_, 因为我们的视觉进化导致我们对太阳光中含量最多的红、绿、蓝三种波长的光最为敏感。 卫星传感器能够感知更广泛的电磁波谱。 传感器这种能能感知人类视觉范围以外光的能力，使得我们可以变不可见为可见。

电磁波谱的范围是如此的广泛，以至于一个传感器同时收集所有波长的信号是不切实际的。 取而代之，人们使用不同的传感器去采集特定波长的电磁波谱。波谱被传感器采集和分类的每一个区间被称为一个_波段_。

波段信息的变化可以被编译为不同类型的合成图像，每一种都能突出一种物理属性。 Mapbox 卫星影像主要依赖组成红，绿，蓝光的1,2和3波段。

### 卫星资源

Mapbox 卫星影像基于缩放级别和地理可用性有不同的来源： 

- **Zoom levels 0-8** 使用来自于 NASA MODIS 卫星的[de-clouded](https://www.mapbox.com/blog/improving-mapbox-satellite-by-making-clouds-disappear/) 数据。
- **Zoom levels 9-12** 使用[NASA/USGS Landsat 5 & 7](https://www.mapbox.com/blog/open-aerial/) 影像。
- **Zoom levels 13+** 使用开源和有版权的混合数据，[Digital Globe](https://www.mapbox.com/blog/digital-globe-partnership/)的数据占世界的大部分， USDA’s NAIP 2011–2013 的数据用于美国，丹麦、芬兰和德国的部分地区使用了开源数据。

卫星影像图层基于数据可用性，通过优化在数据时效性和美观性上达到一个平衡。

在被添加到Mapbox satellite之前，我们所有的影像数据已经被我们的卫星影像团队进行了颜色纠正，优化，并融合到了一个栅格tileset中。 想要了解基本过程，请阅读[卫星影像处理](/help/tutorials/processing-satellite-imagery) 教程。

虽然 Mapbox Satellite 致力于展示最清晰的最高分辨率的影像， 我们也提供拥有最新的全球影像数据的 [Landsat Live](/help/glossary/landsat-live) 基础地图。 Landsat Live 影像 来自于 NASA's Landsat 8 卫星，它们被于16天以内。 我们的实时数据管线从 [Landsat on AWS public dataset](https://aws.amazon.com/public-datasets/landsat/)获取数据并且已经覆盖全球。 查看我们的 [live Landsat tool](https://www.mapbox.com/bites/00145/#8/39.996/25.131) 了解影像的最新更新时间和地点。

## 使用卫星影像

Mapbox satellite 是一个复合影像图层，全球覆盖到16级  (1-2m 分辨率), 地区覆盖到 18级 (0.6-0.3m 分辨率), 精细覆盖到级别21+ (7.5cm+). 有一下几种方法可以在你的项目中使用Mapbox Satellite:

- 在[Mapbox Studio](https://www.mapbox.com/studio-manual/reference/styles/#pick-a-template)将其添加为一个模板style。
- [在 Mapbox Studio将Mapbox Satellite添加为一个图层](https://www.mapbox.com/studio-manual/reference/styles/#new-layer).
-  在任意的[Mapbox's APIs and SDKs](https://docs.mapbox.com) 通过 tileset ID `mapbox.satellite`使用 Mapbox Satellite。
- 使用 tileset ID `mapbox.landsat-live`添加 Landsat 实时影像到你的项目中 。

### 上传卫星影像

如果你有能够更满足你需求的影像数据，你可以使用[Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) 或者 通过 [Mapbox Studio](https://www.mapbox.com/studio) 账户上传数据。 确保上传之前你的影像数据已经转为 [GeoTIFF](/help/glossary/tiff) 格式。一旦你上传了数据，它将会被自动转换为栅格tileset ，之后你可以将它添加到你的项目中。更多的关于上传卫星影像的内容，请阅读[处理卫星影像数据](/help/tutorials/processing-satellite-imagery/) 教程。

### 绘制卫星影像

Mapbox 赞助用户一个许可证为OpenStreetMap绘制卫星影像。以商业目的从Mapbox卫星影像中生成派生矢量数据需要遵循 Mapbox 商业卫星影像许可。详情请[联系我们的销售团队](https://www.mapbox.com/contact/sales/) 。

## 提供卫星影像反馈

如果你发现哪一部分影像需要改进或更新，请通过[imagery request tool](https://www.mapbox.com/imagery-requests)向我们反馈。 这个工具会把你的请求添加到一个 master 列表， 我们对改列表进行优先处理。 如果你想推荐一个影像资源，请在请求中说明。 请标明 这个影像没用被添加到清单中，并且是在何时哪里被更新为可用的。
