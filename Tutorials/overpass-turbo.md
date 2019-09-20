---
title: Add OpenStreetMap data to your Mapbox project
description: Learn how to export OpenStreetMap data to be used in your Mapbox project.
thumbnail: overpassTurbo
level: 2
topics:
- data
- uploads
language:
- No code
prereq: Learn to navigate the OpenStreetMap tagging system.
contentType: tutorial
---

如果您希望在 Mapbox Studio 中使用 [OpenStreetMap](https://www.osm.org/) 数据，请不要再犹豫了！在本指南中，您将学习如何使用 [Overpass Turbo](https://overpass-turbo.eu/) 获取 OpenStreetMap 数据并提取给定区域中的特定要素。您将可以导出[Mt. Bachelor](https://en.wikipedia.org/wiki/Mount_Bachelor) (俄勒冈州中部一个受欢迎的滑雪胜地)的雪地缆车和滑雪路线。如果您想以编程方式而不是用户界面提取 OpenStreetMap 功能，请阅读 [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) 文档以获取更多信息。

## 入门

如果这是您第一次使用OpenStreetMap，我们建议您在开始之前阅读 [我们的地图数据](https://docs.mapbox.com/help/how-mapbox-works/mapbox-data/) 指南中的OpenStreetMap和Mapbox 。

### OpenStreetMap 功能

在OpenStreetMap中，贡献者可以标记建筑物或道路等物理特征以帮助描述它们。例如，要向 `building` 要素添加标记，该要素的关键将是 `building` ，值将是`yes`。

![example of adding a building tag in OpenStreetMap](/help/img/3rdparty/overpass-tag.jpg)

如果我们想要更具体地说明它是什么类型的建筑物，例如酒店，我们可以将标签更改为`building=hotel`。现在，访问数据的其他人将知道该功能是一个建筑物*，*而且它是一个酒店。这对于试图查询特定区域内所有酒店的人尤其有用。

您可以在 [OpenStreetMap Features wiki](http://wiki.openstreetmap.org/wiki/Map_Features) 上找到所有键和值的列表。

### OpenStreetMap 数据 and Mapbox Streets

[Mapbox Streets](https://www.mapbox.com/developers/vector-tiles/mapbox-streets-v7/) 使用OpenStreetMap作为其主要数据源。Mapbox Streets 是一个矢量 [tileset](https://docs.mapbox.com/help/glossary/tileset) ，可供所有 Mapbox 用户使用，几乎可用于所有 Mapbox 模板样式。如果您在 Mapbox Studio 样式编辑器中基于 Mapbox 模板创建新样式，则样式包括 Mapbox Streets tileset。

如果您想在 Mapbox Studio 中使用 OpenStreetMap 数据，最快捷的方法是使用Mapbox Streets作为您样式的源。Mapbox Streets 是根据 OpenStreetMap 数据创建的tileset，随着 OpenStreetMap 的编辑，它会不断更新。要查看您的 Mapbox Streets 版本中包含哪些OpenStreetMap 功能，请访问 [Mapbox Streets文档](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/)。如果要向地图中添加未包含在 Mapbox Streets 中的要素，则需要使用其他工具（如Overpass Turbo）来提取OpenStreetMap数据。

## 使用 OpenStreetMap Wiki

在这个练习中，你将需要找到 Mt. Bachelor Ski Resort 中的一些要素：

- Downhill ski trails
- Chair lifts
- Lift stations

首先，您需要为这些功能找到合适的标签。您可以通过打开 OpenStreetMap 并单击某个功能来查找其标签或搜索 [OpenStreetMap Map Features wiki](http://wiki.openstreetmap.org/wiki/Map_Features) 来完成此操作。搜索 [Wiki](http://wiki.openstreetmap.org/wiki/Map_Features) 以查找与您要查询的功能最相似的键和值。

在 wiki 中，您可以找到以下关键字和我们的功能值：

| **Key**  | **Value**  | **Element**  | **Comment**  |
|---|---|---|---|
| piste:type| downhill |Area/Way| An alpine/downhill ski route. Ways should be used for trails connecting the routes. This automatically implies `oneway=yes`. The direction of the way should be the downhill direction.	|
| aerialway | chair_lift | Way | Looped cable with a series of single chairs or benches, exposed to the open air. Implies `oneway=yes`; where passengers can be carried in the reverse direction, tag with `oneway=no`.|
| aerialway| station	| Node Area| A station, where passengers can enter and/or leave the aerialway|


现在您已拥有正确的键和值，打开 [Overpass Turbo](http://overpass-turbo.eu/) 以查询OpenStreetMap以获取数据。

## 使用 Overpass Turbo

首先快速浏览一下Overpass Turbo的界面。

![screenshot of the Overpass Turbo interface](/help/img/3rdparty/overpass-portland.png)

### Navigate the interface menu

- **Run.** 在代码窗口中运行当前查询。结果将在右侧地图上突出显示。
- **Share.** 指向当前查询的链接。
- **Export.** 将查询的数据导出为不同的格式，以便在其他应用程序中使用。
- **Wizard.** 一个查询向导，允许您根据键和值查找功能。
- **Save.** 保存您的查询以供将来使用。
- **Load.** 加载示例查询或保存的查询。
- **Settings.** 允许您更改界面的地图背景，语言和其他功能。
- **Help.** 有关界面的有用提示和主题。

__Tabs__

- **Map.** 默认地图视图（您可以将背景与其他Web服务交换）。
- **Data.** 原始数据视图。

### Run a query

当你第一次启动 [Overpass Turbo时](http://overpass-turbo.eu/)，它会以一个查询[饮水机](http://overpass-turbo.eu/s/3Xp)的例子开始。Overpass Turbo使用简化版的XQuery来查询OpenStreetMap功能。

您必须单击**”Run“**以在地图上显示结果。执行查询后，Overpass将突出显示符合查询条件的功能。

![Portland drinking fountains](/help/img/3rdparty/overpass-portland-df.png)

仔细查看查询的结构：

```
/*
This is an example Overpass query.
Try it out by pressing the Run button above!
You can find more examples with the Load tool.
*/
node
  [amenity=drinking_water]
  (\{\{bbox\}\});
out;
```

查询首先查找具有该类型的功能 `node` 。然后它 `amenity` 根据值检查密钥 `drinking_water` 。可以发出边界框（西南和东北坐标对），或者在这种情况下， `bbox` 变量将获取当前窗口的范围。

现在您已熟悉 Overpass Turbo 的界面，您可以使用它来获取滑雪功能。

### Find the ski amenities

首先使用搜索工具进行定位 `mt. bachelor, oregon`。搜索工具位于缩放按钮右侧的地图上。

一旦你找到并放大到 Mt. Bachelor，单击工具栏中的**”Wizard“**按钮并在查询向导窗口中粘贴以下语句：

```sql
aerialway=station OR aerialway=chair_lift OR piste:type=downhill
```

这些是我们从OpenStreetMap Features wiki中找到的键和值。单击**Run**。您应该看到Overpass已突出显示地图上的功能。

![screenshot of OverpassTurbo querying ski features](/help/img/3rdparty/overpass-build-query.png)

### 导出数据

现在Overpass找到了这些功能，然后导出它们。单击工具栏中的**“Export”**按钮，选择“ **GeoJSON”**。

![screenshot of the export options in Overpass Turbo](/help/img/3rdparty/overpass-export.png)

您还可以从工具栏中的**“Share”**按钮共享Overpass中的查询。[这是我们保存的查询](http://overpass-turbo.eu/s/f5F)。

## Finished Product

您已经学习了如何使用 Overpass Turbo 从 OpenStreetMap 查询和导出数据！现在您已拥有数据，您可以通过[将数据](https://www.mapbox.com/studio-manual/overview/geospatial-data/)作为[数据集](https://www.mapbox.com/studio-manual/reference/datasets/)或 [tileset](https://www.mapbox.com/studio-manual/reference/tilesets/) 在[Mapbox Studio](https://www.mapbox.com/studio)中[上传](https://www.mapbox.com/studio)，并使用 Mapbox Studio 样式编辑器创建新的自定义样式，开始使用 Mapbox 构建。阅读[ Mapbox Studio 手册](https://www.mapbox.com/studio-manual/)以开始使用。

