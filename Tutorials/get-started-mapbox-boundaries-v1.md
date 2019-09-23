---
title: 开始使用Mapbox Boundaries v1
description: Get started with v1 of the Mapbox Boundaries tileset.
level: 2
platform: web
topics:
- data
language:
- No code
thumbnail: getStartedEnterpriseBoundaries
prereq: Familiarity with front-end development and access to Mapbox Boundaries.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
  <LegacyNote
    legacyProduct='Boundaries v1'
    alternativeResource={{
      title: 'Get started with Mapbox Boundaries',
      link: '/help/tutorials/get-started-enterprise-boundaries/'
    }}
  />
}}

{{
  <Note
    title="Access to Mapbox Boundaries"
    imageComponent={<BookImage />}
  >
    <p>对Mapbox Boundaries tilesets的使用权限受 Mapbox账户的access token所控制。 如果你无法访问你的账户, 请<a href='https://www.mapbox.com/contact/'>联系Mapbox销售代表</a>，以请求使用Boundaries tilesets。</p>
  </Note>
}}

Mapbox Enterprise 用户可以为他们的地图和数据可视化添加 administrative 和 postal 类型 boundaries。此指南包含了如何在web应用程序中使用 Mapbox Boundaries，及要素查找表、数据连接、和切片获取 API。

![image of the Mapbox Boundaries tileset in x-ray mode](/help/img/data/enterprise-boundaries-xray.png)

## 入门

Mapbox Boundaries 作为 Enterprise plan 的一部分提供。如果您没有订购 Enterprise plan，或者您已经拥有Enterprise plan 想要添加 Mapbox Boundaries 的使用权限，请<a href='https://www.mapbox.com/contact/'>联系Mapbox销售代表</a>以请求使用权限。Mapbox Boundaries tilesets 的使用权限受 Mapbox 账户的 access token 所控制。

## 添加到应用程序

倘若您拥有 Mapbox Boundaries 的使用权, 您就可以在应用程序中使用它们，就像使用任何其他的 [tileset](/help/glossary/tileset/) 一样。

### 关于Mapbox Boundaries

您可以在下面找到使用Mapbox Boundaries tileset所需的一些关键信息。

#### Tileset IDs

Mapbox Boundaries作为矢量切片的形式存储并通过 [Mapbox Vector Tiles API](https://docs.mapbox.com/api/maps/#vector-tiles) 分发，每一个 admin 和 postal 级别都具备独有的切片组。每个 Boundaries tilesets 的[Tileset IDs](/help/glossary/tileset-id/) 形如`mapbox.enterprise-boundaries-adminOrPostalLevel-version` 。例如，admin 的 0 级 boundaries (包含国家/地区) 的 tileset ID 为 `mapbox.enterprise-boundaries-a0-v1`。

#### Feature IDs

每个[要素(Feature)](/help/glossary/features/)也拥有唯一的ID，用以区分要素多边形。倘若您已经将 Boundaries 添加到您的账户，你就可以访问包含 feature IDs 和 所有标记元数据的参考文档。

#### 最小缩放级别和边界框

- **z_min**：每个要素的`z_min` 值标记了 tileset 中要素可用的最小 [缩放级别(zoom level)](/help/glossary/zoom-extent/)。您可以使用该选项来设置可以查看某一要素的最小的相机缩放级别。
- **centroid point**：Centroid point 要素会在缩放级别达到 `z_min` + 1时出现。Centroid point 要素可以用于在 Boundaries 要素的中心中展示标记(marker)、符号(symbol)、标签(label)。
- **bounds**：要素边界(bounds) 是覆盖所有要素的最小矩形，可以通过数组 `[min_long, min_lat, max_long, max_lat]` 的形式表示。


### 示例

要在您的应用程序中使用 Mapbox Boundaries tileset，请从 Mapbox Vector Tiles API 中发出相关 tileset的请求。例如，在 Mapbox GL JS 中加载 tileset 的代码如下所示：

```js
// Be sure to use an access token from an account
// that has access to Boundaries
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  center: [-99.9, 41.5],
  zoom: 1
});

map.on('load', function() {

  // Add source for admin-0 Boundaries
  map.addSource('admin-0', {
    type: 'vector',
    url: 'mapbox://mapbox.enterprise-boundaries-a0-v1'
  });
  // Add a layer with boundary lines
  map.addLayer({
    id: 'admin-0-line',
    type: 'line',
    source: 'admin-0',
    'source-layer': 'boundaries_admin_0',
    paint: {
      'line-color': 'red',
      'line-width': ['interpolate', ['linear'], ['zoom'], 0, 2, 20, 10]
    }
  }, 'waterway-label');
  // Add a layer with points
  map.addLayer({
    id: 'admin-0-circle',
    type: 'circle',
    source: 'admin-0',
    'source-layer': 'points_admin_0',
    paint: {
      'circle-color': 'white',
      'circle-stroke-color': 'black',
      'circle-stroke-width': ['interpolate', ['linear'], ['zoom'], 0, 2, 20, 6],
      'circle-radius': ['interpolate', ['linear'], ['zoom'], 0, 2, 20, 20]
    }
  }, 'waterway-label');
});
```

上面的代码将生成一个所有国家/地区边界为红色、国家/地区中心有一个圆圈的世界地图。

![a map with all country boundaries in red with a circle at the center of each country](/help/img/data/enterprise-boundaries-sample.png)

## 要素查找表(lookup tables)

每个 boundary 要素都在查找表(lookup table) 中编制索引。查找表仅在您的应用程序内部使用。用户数据可以添加到您应用程序中的 Mapbox Boundaries 中，以创建可视化，例如一幅州际失业率等值图。

### 关于要素查找表

Mapbox Boundaries 的查找表包括以下有关每个多边形要素的元数据：

- **id**：要素的全局唯一标识符
- **level**: 级别，包括admin level; admin-0, admin-1....post-3, post-4
- **country_code**: 国家/地区代码，2位 ISO 代码
- **name**：本地要素名称
- **name_ascii**：转换为 ASCII 字符的本地要素名称。
- **admin_code**：要素的 admin 或 postal 代码
- **bounds**：要素盒型边界（bounding box）的数组 `[minlong, minlat, maxlong, maxlat]`。
- **z_min**：多边形要素在 tileset 中显示的最小缩放级别。
- **parent_0**：要素的0级父级(如果存在)。
- **parent_1**：要素的1级父级(如果存在)。
- **parent_2**：要素的2级父级(如果存在)。
- **parent_3**：要素的3级父级(如果存在)。
- **parent_4**：要素的4级父级(如果存在)。
- **tileset_name**：包含该要素的切片组的序号。
- **point_layername**：切片组中，包含要素中心（centroid）的 source-layer 名称。
- **poly_layername**：切片组，包含多边形要素几何的 source-layer 的名称。

查找表以两种形式提供：`tsv` 和 `json`。

### 示例工作流程

要素查找表旨在与Mapbox Boundaries tilesets一起使用。商业智能应用程序的典型工作流程是：

1. 用户识别数据源中的地理维度，例如州，邮政编码，国家/地区或经度和纬度。
2. 用户从应用程序数据存储进行查询。
3. 数据存储器连接地理维度查询结果的元数据中的要素查找表，例如`name`，`unit_code`，或`level`。
4. 数据存储按地理维度分类总计结果，并发送到客户端可视化工具。
5. 从Mapbox样式规范生成Mapbox GL图层，以根据查询结果创建可视化。
6. 视觉样式定义在所有Mapbox GL产品中的工作方式都是相同的，包括Web上的Mapbox GL JS和iOS，Android，macOS和Qt上的Mapbox GL Native。

### 示例

阅读 [可视化美国经济复苏与客户端数据加入](https://blog.mapbox.com/visualize-the-usas-economic-recovery-with-client-side-data-joins-2aeab23ee9b0) 博客文章，其中说明了示例工作流程中的步骤如何在您的应用程序中工作。

## 数据连接（Data-joins）

### 关于 数据连接（data-joins）

数据连接（ data-join ）技术是本地数据（例如美国各州的失业率）与数据驱动样式的矢量切片要素之间的内部连接。 

### 示例工作流程

要创建数据连接，可以使用以下流程：

- 初始化Mapbox符号样式对象，这是数据驱动的图层填充颜色样式。

```
var color_dds = { "property": "id", "type": "categorical", "default": "rgba(0, 0, 0, 0)", //Set the default color to opacity zero "stops": [] }
```

- 为需要可视化的要素设置一个形如 `[id, style value]` 数组，这个数组是数据节点的列表。

```
color_dds.stops = [['US', 'red'], ['UK', 'green']]
```

- 只有在`color_dds.stops` 中有对应id的要素才会在可视化中显示。
- 设置图层的 paint 属性来实现可视化。

```
map.setPaintProperty('my-layer-name', 'fill-color', color_dds)
```

### 示例

探索此 [示例代码](https://www.mapbox.com/mapbox-gl-js/example/data-join/) 来应用数据连接技术，用于从连接到Boundaries的用户数据创建一副等值地图。


## Point-in-polygon 查询

### 关于 Tilequery

使用 [Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#retrieve-features-from-vector-tiles) 来使点和多边形相匹配。示例请求如下：

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a0-v1/tilequery/{longitude,latitude}.json?access_token={{ <UserAccessToken /> }}
```

如果点在多边形内，则 Tilequery API response 会返回 GeoJSON 格式的 body。返回的第一个要素的id属性值是包含查询点的 Boundaries 要素的ID。

由于要素查找表包含所有的 Mapbox Boundaries 父要素，因此每个点只需要一个API请求来查找所有匹配的父边界。例如，您可以查询意大利某个点的admin-3边界，并使用查找表在admin-2，admin-1和admin-0中查找父要素。

### 示例

以下是从意大利的示例查询到admin-3的示例API响应。查询URL是：

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a3-v1/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

返回的 `id` 是含有该点的 admin-3 边界要素的标识符。

```json
{
  "type": "FeatureCollection",
  "features": [{
    "type": "Feature",
    "geometry": {
      "type": "Point",
      "coordinates": [
        12.87,
        43.1
      ]
    },
    "properties": {
      "id": "ITA3054034",
      "tilequery": {
        "distance": 0,
        "layer": "boundaries_admin_3"
      }
    }
  }]
}
```

你可以使用 tile compositing 功能，在一个 API 调用中查询多个 admin 级别。以下查询将会返回某位置的 admin-1、admin-2 和 admin-3 的  `admin_ids` 。

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a3-v1,mapbox.enterprise-boundaries-a2-v1,mapbox.enterprise-boundaries-a1-v1/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

此技术允许在任何 admin 级别或多个 admin 级别中聚合和可视化点，并使其成为单个的点，用作 API 服务。

### 示例

你可以尝试以下端到端的 [同时使用数据连接和Tilequery API的示例](https://www.mapbox.com/labs/vt-polygons/).

![an end to end example using the data-join technique and Tilequery API](/help/img/data/enterprise-boundaries-choropleth-demo.gif)

## 下一步

你可以使用应用程序所用的任何自定义数据来扩展  Mapbox Boundaries。这意味着为您的应用程序添加学区、城市、市场或属性边界——所有这些都具有与原生产品相同的性能和 API 功能。更多相关信息请阅读 [Extend Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/) 教程。
