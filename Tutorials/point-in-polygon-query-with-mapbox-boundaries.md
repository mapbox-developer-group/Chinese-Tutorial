---
title: Point-in-polygon query with Mapbox Boundaries
description: Query data in v2 of the Mapbox Boundaries tileset.
level: 2
topics:
- data
language:
- JavaScript
thumbnail: pointInPolygonQueryWithEnterpriseBoundaries
prereq: Familiarity with front-end development and access to Mapbox Boundaries.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
<Note
  title="使用Mapbox边界"
  imageComponent={<BookImage />}

>  <p>对Mapbox Boundaries tilesets的使用权由Mapbox帐户令牌控制。如果您无法使用自己的帐户，请<a href='https://www.mapbox.com/contact/'>与Mapbox销售代表联系</a>，以请求使用Boundaries tilesets。</p>

</Note>
}}

Mapbox Enterprise 用户可以为其地图和数据可视化添administrative, postal, 或 statistical boundaries。本指南介绍了如何使用Mapbox边界和Mapbox Tilequery API来查询多边形中的点。

## 入门

Mapbox Boundaries作为 Enterprise plan 的一部分提供。如果您没有 Enterprise plan，或者您有 Enterprise plan 并且想要添加对Mapbox Boundaries的使用权限，请 [联系Mapbox销售代表](https://www.mapbox.com/contact/) 以请求权限。对 Boundaries tilesets 的使用权限由您的 Mapbox 帐户令牌控制。

## 关于 Tilequery API

[Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) 允许你从 tileset 中获取数据，而不必渲染地图。您可以使用 Tilequery API 将点与多边形匹配，换句话说，您可以提供点的坐标并确定指定 tileset 中存在哪些（如果有的）多边形。

以下是使用 Boundaries tileset 的 Tilequery API 请求的可能形式：

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a0-v2/tilequery/{longitude,latitude}.json?access_token={{ <UserAccessToken /> }}
```

{{
  <Note imageComponent={<BookImage />}>
    <p>请务必使用有权使用 Mapbox Boundaries 的帐户令牌。</p>
  </Note>
}}

如果指定的点在多边形内，则 Tilequery API 响应将包含一个 GeoJSON 格式的 body，其中包含 tileset 中的所有要素。`id` 返回的第一个要素的属性值是包含查询点的 Boundaries 要素的ID。

由于要素查找表包含所有 Mapbox Boundaries 父要素，因此每个点只需要一个 API 请求来查找所有匹配的父边界。例如，您可以查询意大利某个点的 admin-2 级别 boundary，并使用查找表在 admin-1 和 admin-0 中查找父级要素。

## Query Mapbox Boundaries

以下是从意大利的示例查询到 admin-2 的示例 API 响应。查询URL是：

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a2-v2/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

{{
  <Note imageComponent={<BookImage />}>

请务必使用有权使用 Mapbox Boundaries 的帐户令牌。

  </Note>
}}

所述`id`返回是含有点要素的 admin-2 的 Boundaries 的标识符。

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          12.87,
          43.1
        ]
      },
      "properties": {
        "id": "ITA2054",
        "worldview": "all",
        "tilequery": {
          "distance": 0,
          "geometry": "polygon",
          "layer": "boundaries_admin_2"
          }
      }
    }
  ]
}
```

### Query multiple tilesets

您可以使用 tile compositing  在一个 API 调用中查询多个管理级别。下面的查询将位置的 admin-1，admin-2 和 admin-3  的`id`s 返回：

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a3-v2,mapbox.enterprise-boundaries-a2-v2,mapbox.enterprise-boundaries-a1-v2/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

{{
<Note
  imageComponent={<BookImage />}

>  <p>在<a href="https://www.mapbox.com/vector-tiles/enterprise-boundaries-v2">参考文档</a>中找到Boundaries tilesets的完整列表。</p>

</Note>
}}

此技术允许在任何  admin 级别或多个 admin 级别聚合和可视化点，直至各个点，作为API服务。

## Next steps

### 关于 Tilequery API 了解更多

使用我们的 [创建时区查找器](https://docs.mapbox.com/help/tutorials/create-a-timezone-finder-with-mapbox-tilequery-api/) 教程构建一个应用程序，用于确定您使用 Mapbox Tilequery API 和本机 HTML 地理位置 API [的时区](https://docs.mapbox.com/help/tutorials/create-a-timezone-finder-with-mapbox-tilequery-api/)。

### 关于Mapbox Boundaries 了解更多

详细了解如何使用Mapbox Boundaries。

- [Data-joins with Mapbox Boundaries](/help/tutorials/data-joins-with-enterprise-boundaries/): 数据连接技术涉及本地数据(如美国各州的失业率)和矢量切片要素(如 Mapbox Boundaries 中 admin boundaries )，并使用数据驱动的样式表示。
- [Extend Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/): 您可以使用应用程序所需的任何自定义数据扩展 Mapbox Boundaries。这可能意味着为您的应用程序添加学区，城市，市场或属性边界 - 所有这些都具有与本机产品相同的性能和API功能。

### 高级用例

您还可以探索此 [端到端示例](https://www.mapbox.com/labs-sandbox-demos/vt_polygons/) ，该 [示例](https://www.mapbox.com/labs-sandbox-demos/vt_polygons/) 使用此多边形点查询教程和 [数据连接](https://docs.mapbox.com/help/tutorials/data-joins-with-enterprise-boundaries/) 教程中概述的概念来创建交互式等值图的应用程序。

![an end to end example using the data-join technique and Tilequery API](/help/img/data/enterprise-boundaries-choropleth-demo.gif)
