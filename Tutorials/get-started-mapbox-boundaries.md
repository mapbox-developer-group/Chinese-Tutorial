---
title: Get started with Mapbox Boundaries
description: Get started with v2 of the Mapbox Boundaries tileset.
category: Tutorials
level: 2
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
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
  <Note imageComponent={<BookImage />}>
    <p>对Mapbox Boundaries tilesets的使用权限受Mapbox账户的access token所控制。 如果你无法访问你的账户，请 <a href='https://www.mapbox.com/contact/'>联系Mapbox销售代表</a>，以请求使用Boundaries tilesets。</p>
  </Note>
}}

Mapbox Enterprise用户可以为其地图和数据可视化添加administrative、postal和statistical boundaries。本指南介绍了如何在Web应用程序中使用Mapbox Boundaries和要素属性表。

![image of the Mapbox Boundaries tileset in x-ray mode](/help/img/data/enterprise-boundaries-xray.png)

## 入门

Mapbox Boundaries 作为 Enterprise plan 的一部分提供。如果您没有订购 Enterprise plan，或者您已经拥有Enterprise plan 想要添加 Mapbox Boundaries 的使用权限，请 <a href='https://www.mapbox.com/contact/'>联系Mapbox销售代表</a> 以请求使用权限。对 Mapbox Boundaries tilesets 的使用权限受 Mapbox 账户的 access token 所控制。

## 添加到应用程序

倘若您拥有 Mapbox Boundaries 的使用权，您就可以在应用程序中使用它们，就像使用任何其他的 [tileset](/help/glossary/tileset/) 一样。

### 关于Mapbox Boundaries

您可以在下面找到使用Mapbox Boundaries tileset所需的一些关键信息。

#### Tileset IDs

Mapbox Boundaries作为矢量切片的形式存储并通过 [Mapbox Vector Tiles API](https://docs.mapbox.com/api/maps/#vector-tiles) 分发。每一个admin、stats、和 postal level 都有不同的 tileset。Boundaries tilesets的 [Tileset IDs](/help/glossary/tileset-id/) 保存在此表单中： `mapbox.enterprise-boundaries-{a|p|s}{level}-{version}`。这里有一些例子：

- `mapbox.enterprise-boundaries-a0-v2`：此 tileset 是提供给 admin (`a`) level 0 (`0`) 的边界图层 （也包含了国家/地区），属于 version 2 (`v2`) 的 Mapbox Boundaries。
- `mapbox.enterprise-boundaries-p1-v2`：此 tileset是提供给 postal (`p`) level 1 (`1`) 的边界图层，属于 version two (`v2`) 的 Mapbox Boundaries。
- `mapbox.enterprise-boundaries-s3-v2`：此 tileset 是提供给 stats (`s`) level 3 (`3`) 的边界图层， 属于 version two (`v2`) 的 Mapbox Boundaries。

**您可以在 [参考文档](https://www.mapbox.com/vector-tiles/enterprise-boundaries-v2/) 中获得Mapbox Boundaries tilesets的完整列表，并可深入阅读关于tileset层次结构的内容。**

#### Feature IDs

每个 [要素（Feature）](/help/glossary/features/)也拥有唯一的ID，用以区分要素多边形。倘若您已经将 Boundaries 添加到您的账户，你即可以可以访问包含 feature IDs 和 所有标记元数据的参考文档。

#### 最小缩放级别和边界框

- **z_min**：每个要素的 `z_min` 值标记了 tileset 中要素可用的最小 [缩放级别（zoom level）](/help/glossary/zoom-extent/)。您可以使用该选项来设置可以查看某一要素的最小的相机缩放级别。
- **centroid point**：Centroid point 要素会在缩放级别达到 `z_min` + 1时出现。Centroid point 要素可以用于在 Boundaries 要素的中心中展示标记（marker）、符号（symbol）、标签（label）。
  - 使用 [上述的tileset ID](#tileset-ids) 并指定 [源层（source layer）](/help/glossary/source-layer/) `points_{admin|postal|stats}_{level}` 来使用包含用于特定admin、postal或stat level的centroid points。例如，矢量切片源层 `points_postal_4` 包含了用于  `mapbox.enterprise-boundaries-p4-v2` 的centroid point 切片组。
- **bounds**：要素边界（bounds） 是覆盖所有要素的最小矩形，可以通过数组 `[min_long, min_lat, max_long, max_lat]` 的形式表示。


### 示例

要在您的应用程序中使用 Mapbox Boundaries tileset，请从 Mapbox Vector Tiles API 中发出相关tileset的请求。例如，在 Mapbox GL JS 中加载 tileset 的代码如下所示：

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
    url: 'mapbox://mapbox.enterprise-boundaries-a0-v2'
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

上面的代码将生成一张所有国家/地区的边界为红色并且每一个国家/地区的中心都有一个圆圈的世界地图。

![a map with all country boundaries in red with a circle at the center of each country](/help/img/data/enterprise-boundaries-sample.png)

## 要素查找表（lookup tables）

每个 boundary 要素都在查找表（lookup table） 中编制索引。查找表仅在您的应用程序内部使用。用户数据可以添加到您应用程序中的 Mapbox Boundaries 中，以创建可视化，例如一幅州际失业率等值图。

### 关于要素查找表

Mapbox Boundaries 的查找表包括以下有关每个面要素的元数据：

- **id**：要素的全局唯一标识符。
- **id_int**：要素的一个整数标识符，可用于与 [Mapbox GL JS's feature state](https://www.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate) 进行数据连接。
- **type**：`admin`、 `postal` 或 `stats` 中的一种，用于表示 Mapbox Boundaries 属于 Administrative、 Postal 或 Statistical 边界类型。
- **level**：0-5中的一个数字，用于表示类别中边界的界别。
- **layer**：一个类型（type）和级别（level）的缩写，包含要素的类型，即 administrative (`a`)、postal (`p`) 和  statistical (`s`) 和级别 (`0-5`) 。例如，administrative 的 1 级别用 `a1` 表示。
- **tilesetname**：包含要素的 tileset 的标识符，详见 [参考文档](https://docs.mapbox.com/vector-tiles/reference/mapbox-boundaries-v2/#tilesets)。
- **worldview**：根据区域地图显示要求 （`US`、 `CN` 或 `IN`）交替显示行政单位。
- **unit_code**：要素所使用的国家/地区专用标识符，例如邮政编码或 FIPS 代码。
- **name**：本地要素的名称。
- **name_ascii**：转换为 ASCII 字符的本地要素名称。
- **names**：该 boundary 的任何翻译名称或别名。
- **description**：与每个国家/地区的 boundary 结构相对应的文本限定符。例如，美国 admin-1 级别的boundaries 有 `states` 的描述，而意大利 admin-1 级别的 boundaries 有 `regions` 的描述。
- **wikidata_id**：与该 boundary 相对应的 [Wikidata ID](https://www.wikidata.org/wiki/Wikidata:Main_Page)。
- **source_date**：boundary 数据的更新日期。
- **parent_0**：与国家/地区代码对应的要素的0级父级。
- **parent_1**：要素的一级父级(如果存在)。
- **parent_2**：要素的二级父级(如果存在)。
- **parent_3**：要素的三级父级(如果存在)。
- **parent_4**：要素的四级父级(如果存在)。
- **z_min**：polygon 要素在 tileset 中显示的最小缩放级别。
- **centroid**：`[long, lat]` 格式 boundary 的质心。
- **bounds**：要素盒型边界的数组 `[minlong, minlat, maxlong, maxlat]`。
- **polylayername**：包含 polygon 要素的 tileset 的 source-layer 的名称。
- **pointlayername**：包含 polygon 要素质心的 tileset 的 source-layer 的名称。

查找表以JSON的形式提供。

### 示例工作流程

要素查找表旨在与Mapbox Boundaries tilesets一起使用。商业智能应用程序的典型工作流程是：

1. 用户识别数据源中的地理维度，例如州、邮政编码、国家/地区或经度和纬度。
2. 用户从应用程序数据存储进行查询。
3. 数据存储器连接地理维度查询结果的元数据中的要素查找表，例如 `name`、`unit_code` 或 `level`。
4. 数据存储按地理维度分组和分类结果，并发送到客户端可视化工具。
5. 从Mapbox样式规范生成Mapbox GL图层，以根据查询结果创建可视化。
6. 视觉样式定义在所有Mapbox GL产品中的工作方式相同，包括Web上的Mapbox GL JS和iOS、Android、macOS和Qt上的Mapbox GL Native。

### 示例

阅读 [可视化美国经济复苏与客户端数据加入](https://blog.mapbox.com/visualize-the-usas-economic-recovery-with-client-side-data-joins-2aeab23ee9b0) 博客文章，其中说明了示例工作流程中的步骤如何在您的应用程序中工作。

## 下一步

详细了解如何使用Mapbox边界：

- [使用 Mapbox Boundaries 的多边形点查询](https://docs.mapbox.com/help/tutorials/point-in-polygon-query-with-enterprise-boundaries/)：使用Mapbox Tilequery API确定单个点上存在的polygon。
- [与 Mapbox Boundaries 的数据连接](/help/tutorials/data-joins-with-enterprise-boundaries/)：数据连接技术涉及本地数据（如美国各州的失业率）和矢量切片要素（如 Mapbox Boundaries 中 admin boundaries），并使用数据驱动的样式表示。
- [扩展 Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/)：您可以使用应用程序所需的任何自定义数据扩展 Mapbox Boundaries。这可能意味着为您的应用程序添加学区、城市、市场或属性边界——所有这些都具有与本机产品相同的性能和API功能。
