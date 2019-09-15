---
title: Geocoding 地理编码
description: Learn how geocoding works and how to use geocoding in your next Mapbox project.
image: /img/narrative/geocoding.svg
topics:
  - geocoding
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import ChevronousText from '@mapbox/mr-ui/chevronous-text';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: guide
---

The [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) performs two main tasks: *forward geocoding* and *reverse geocoding*. Forward geocoding converts text into geographic coordinates, for example, turning `2 Lincoln Memorial Circle NW` into `-77.050,38.889`. Reverse geocoding converts geographic coordinates into a text description, for example, turning `-77.050,38.889` into `2 Lincoln Memorial Circle NW`.

[Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 主要执行两大任务：*正向地理编码* 和 *反向地理编码*。正向地理编码将地址文本转换成相应的地理坐标，例如，将 `2 Lincoln Memorial Circle NW` 转换为 `-77.050,38.889`。反向地理编码则是指将地理坐标转化为地址文本说明的过程，例如，将 `-77.050,38.889` 转化为 `2 Lincoln Memorial Circle NW`。

All geocoding requests require you to submit a *query*, or what you're trying to find. When you make a query, you get a *response*, a JSON-formatted document of the most relevant results from your query. This guide provides an overview of how the Geocoding API works, how to use it, how to provide feedback, and links to relevant documentation to get you started.

所有的地理编码请求都需要您提交一个 *查询* 请求，换言之，您需要告诉API您即将查找的地点。当您发出一个查询请求，您将获得一则以JSON文件格式出现的 *回复* 信息。这则 *回复* 记录了与查询请求最相关的查询结果。本篇指南将为您介绍：Geocoding API如何运作，如何使用Geocoding API，以及如何提交相关的反馈意见给Mapbox。您可以参考本篇指南最后的相关文档来开始使用Mapbox地理编码服务。

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-geocoding-works.html" />
}}

Here's an example that uses the [Mapbox GL geocoder plugin](https://github.com/mapbox/mapbox-gl-geocoder) to add forward geocoding to a web app built with Mapbox GL JS. Type in a location to view the raw JSON response for that query. Geocoding results are returned in [Carmen GeoJSON](https://github.com/mapbox/carmen/blob/master/carmen-geojson.md) format and contain both descriptive location information and geographic information. You can use the geographic information returned in the JSON response to show your query on a map, like in this example, or do additional spatial analysis.

本示例使用了 [Mapbox GL geocoder 插件](https://github.com/mapbox/mapbox-gl-geocoder) 将正向地理编码功能添加到了一个由Mapbox GL JS创建的网页应用中。输入一个地址，您便可以在地图下方查看本次查询所返回的原始JSON代码回复信息。地理编码查询结果会以 [Carmen GeoJSON](https://github.com/mapbox/carmen/blob/master/carmen-geojson.md) 的格式返回，它既包含了描述性位置信息，又包含了地理信息。您可利用JSON回复中的地理信息，将查询请求及结果显示在地图上，正如本示例所展示的那样。您还可以利用所返回的地理信息另外进行空间分析。

## How geocoding works
## 地理编码如何运作

The [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) has two distinct parts: the **source data** we use to define locations and the **tools** we use to search for and return those locations.

[Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 有两个截然不同的组成部分：一个是我们用来定义地点位置的源数据，另一个是我们用来搜索并返回地点信息的工具箱。

### Source data
### 源数据

The Mapbox Geocoding API contains [data sources](https://www.mapbox.com/about/maps/#data-sources) from governments, open data projects, and private companies. In some cases, results from the Geocoding API may differ from [Mapbox Streets](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/) or OpenStreetMap data.

Mapbox Geocoding API 包含了来自政府机构，开源数据项目及私营公司的 [源数据](https://www.mapbox.com/about/maps/#data-sources)。在某些情况下，Geocoding API 返回的查询结果与 [Mapbox Streets](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/) 或者 OpenStreetMap 数据不太一致。

The Mapbox Geocoding API source data contains the following types of geographic information, ordered from the most granular to the largest:

Mapbox Geocoding API 源数据包含了以下几种地理信息（排列顺序根据元素特征自点到面，由小至大）：

- **Points of interest (POI):** A named place including commercial businesses, public buildings, monuments, and parks, among other features.
- **Address:** A specific mailing address, including the address number if applicable.
- **Neighborhood:** A colloquial name for a smaller area within a place. Neighborhoods do not necessarily have specific, legally defined boundaries. Only present in some countries.
- **Locality:** An administrative unit that is smaller than a place. Only present in some countries.
- **Postcode:** A geographic area of the address component used for sorting mail.
- **Place:** Cities, towns, and villages. Note that some large cities (such as Tokyo and Istanbul) may be categorized as regions rather than places.
- **District:** An administrative unit that is larger than a place but smaller than a region. Only present in some countries.
- **Region:** States, provinces, and prefectures. This is typically the largest sub-national administrative unit of a country. Note that some large cities (such as Tokyo and Istanbul) may be categorized as regions rather than places.
- **Country:** Generally recognized countries or, in some cases like Hong Kong, an area of quasi-national administrative status that has been given a designated country code under ISO 3166-1.

- **兴趣点 POI（Points of Interest）：** 一个有名称的地点，它可以是包含在其余地理信息要素中的商务楼，公共建筑，纪念碑/历史遗迹和公园。
- **地址 Address：** 一个具体的邮寄地址，包含门牌号或建筑物号码（如果适用）。
- **街区 Neighborhood：** 一个地方子区域的俗称。街区不一定有确切、法定的边界。仅于某些国家或地区的地址中出现。
- **本地居民区 Locality：** 一个小于地方的行政区域单位。仅于某些国家或地区的地址中出现。
- **邮政行政区（以邮编代表）Postcode：** （邮编）作为地址中的一部分，描述用来分理邮件的地理区域。
- **地方 Place：** 以城市或村镇为代表。请注意，一些大城市（例如，东京和伊斯坦布尔）可被归类为区域而不是地方。
- **区级行政区 District：** 一个比地方大，同时又比区域小的行政区域单位。仅于某些国家或地区的地址中出现。
- **区域 Region：** 以州，省和县为代表。通常它是一个仅次于国家的最大行政区域单位。值得注意的是，一些大城市（例如，东京和伊斯坦布尔）可被归类为区域而不是地方。
- **国家或地区 Country：** 一般指公认的国家，或者一些情况下也指地区， 如：香港特别行政区。它们都有指定的 ISO 3166-1 国家或地区编码。

This hierarchy of feature types is also used to determine what will be returned as the encompassing parent features in a Geocoding API response object's [`context` 属性](https://docs.mapbox.com/api/search/#geocoding-response-object). For example, if the returned feature is a `place` (like Detroit), then the encompassing parent features in the `context` property will be the `region` (the state of Michigan) and the `country` (United States).

这个有关要素类别的层级结构也可以被用来决定一个 Geocoding API JSON回复对象中 [`context` 属性](https://docs.mapbox.com/api/search/#geocoding-response-object) 所包含的父要素。举个例子，如果返回的要素是一个 `place` （如：底特律），那么其 `context` 属性将会是 `region` （密歇根州） 和  `country` (美国)。


### Tools
### 工具

The Mapbox Geocoding API uses [Carmen](https://github.com/mapbox/carmen), an open source project for Mapnik vector tile-based geocoding. For more on Carmen, see [How does Carmen work?](https://github.com/mapbox/carmen#how-does-carmen-work).

Mapbox Geocoding API 使用 [Carmen](https://github.com/mapbox/carmen)，它一个为基于Mapnik矢量切片的地理编码发起的开源项目。更多有关Carmen的内容，请见 [Carmen是如何运作的？](https://github.com/mapbox/carmen#how-does-carmen-work)。

### Customizing your queries
### 自定义您的查询请求

The Mapbox Geocoding API accepts many optional parameters. You can use these optional parameters to customize your queries so that the most relevant results are returned. These parameters can be specified using URL query parameters, or they can be specified as options with one of our client-side libraries or plugins. These parameters allow you to view results as you type, filter results by geographic feature type, and limit or bias results to a specified area. For example, to limit your search results to addresses in the Washington DC Metro area, you could set the `type` parameter to `address` and the `bbox` parameter to `-77.08,38.90,-76.99,38.95`. With those parameters set, your query for `Constitution Ave` will only return street addresses in the DC Metro area, and will not include features you're not interested in (like `Constitution Ave, El Paso, Texas 79908, United States`).

Mapbox Geocoding API 接受多种可选参数。您可以使用这些可选参数来自定义您的查询请求以便返回最相关的查询结果。这些参数可以根据URL中的查询参数来指定，也可以根据任意一个我们客户端库或者插件中的选项来指定。这些参数允许您边输入边查看相关查询结果，根据地理元素类来筛选结果，以及将结果限定在指定地区。例如，若您想将搜索查询结果限制在华盛顿特区都市区内，您可以首先将 `type` 参数设为 `address`, `bbox` 参数设为`-77.08,38.90,-76.99,38.95`。有了这些参数设置，您的输入查询地点 `Constitution Ave` 将会返回限定在华盛顿特区都市区内的相关街道地址，它们并不会包含您不感兴趣的地理元素（如，位于德克萨斯州的 `Constitution Ave`， `Constitution Ave, El Paso, Texas 79908, United States）

Read the [Geocoding API documentation](https://docs.mapbox.com/api/search/#geocoding) for more information on available features.

阅读 [Geocoding API 文档](https://docs.mapbox.com/api/search/#geocoding) 来详细了解更多Geocoding API的功能特征。

### Language support
### 语言支持

The Mapbox Geocoding API accepts a `language` query parameter, which allows you to specify the language in which you would like to search. One or more languages can be specified using [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). Translation availability varies by language and region, and you can expect more consistent results for areas where the specified language is most widely used. Language support has three different levels:

Mapbox Geocoding API 接受一个 `language` 语言查询参数，它允许您指定用来查询搜索的语言。一种或多种语言可以根据 [ISO 639-1 代码](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 来指定。翻译的可用性因语言种类和地区而异，您可以期待从那些指定语言使用广泛的地区中获得更加一致的查询结果。语言支持有三个级别：

- **Global coverage.** These languages are almost always present for `country`, `region`, and prominent `place` features.
- **Local coverage.** These languages may lack global coverage, but they are almost always present for `country`, `region`, and prominent `place` features where they are widely used.
- **Limited coverage.** These languages are sometimes present, but coverage tends to be inconsistent or geographically constrained.

- **全球覆盖：** 这些语言通常都能显示并支持定义 `country`, `region`, 和显著常见的 `place` 这类元素。
- **局部覆盖：** 这些语言尽管没有覆盖全球范围，但是它们通常也可以在广泛使用这些语言的地区显示并支持定义 `country`, `region`, 和显著常见的 `place` 这类元素。
- **有限覆盖：** 这些语言有时会显示，但是其覆盖范围趋于不一致或者受到地理位置限制。


For a current list of the languages covered at each level, see the [Geocoding API documentation](https://docs.mapbox.com/api/search/#language-coverage).

若您有兴趣了解Mapbox Geocoding API有关不同级别语言覆盖范围的最新信息，请见 [Geocoding API 文档](https://docs.mapbox.com/api/search/#language-coverage)。 

### Search result prioritization
### 查询结果优先次序

Results from geocoding queries are prioritized differently depending on whether the request was a _forward geocode_ or a _reverse geocode_.

根据查询请求是否为_forward geocode_ 或 _reverse geocode_，Mapbox Geocoding API会以不同的方式来决定地理编码查询服务结果的优先次序。

#### Result prioritization in forward geocoding
#### 正向地理编码中的结果优先次序

When a forward geocoding query (human-readable text like “San Francisco”) is submitted to the Mapbox Geocoding API, the geocoder uses Carmen, a text search engine, to search our spatial indexes for features that match the user’s query. (For a more detailed description of how the Carmen text search engine works, read the [Carmen documentation](https://github.com/mapbox/carmen/blob/master/docs/how-carmen-works.md).) The geocoder applies filters on the backend to sort the results that match, or partially match, the searched text. These filters are _textual relevance_ and _prominence score_.

当一个正向地理编码请求被提交至Mapbox Geocoding API （例如，可读的文本请求 “旧金山”），地理编码器将使用Carmen， 一个文本搜索引擎，来搜索与用户请求相匹配的元素所对应的空间索引（想了解更多Carmen文本搜索引擎如何工作的相关内容，请阅读 [Carmen 文档](https://github.com/mapbox/carmen/blob/master/docs/how-carmen-works.md)）。地理编码器将在后端使用过滤器来将与搜索文本匹配的或部分匹配的结果进行排序。这些过滤器包括_textual relevance 文本相关性_ 和 _prominence score 显著普遍性分数_。

##### Textual relevance
##### 文本相关性

When the geocoder sorts and prioritizes results, the first filter that is applied is `relevance`. `relevance` is a value that indicates how well a feature in our dataset matches the query. This property is surfaced in the Geocoding API response, and is a numerical score from `0` (the result does not match the queried text at all) to `1` (the result matches the queried text most completely). You can use the `relevance` property to remove results that don't fully match the query.

当地理编码器对查询结果进行排序并决定显示的优先次序时，第一个使用的过滤器是 `relevance`，相关性。 `relevance` 是一个可以表示数据集中元素与查询文本匹配程度的数值。这一属性在Geocoding API的回复结果中就有所体现，它是一个介于 `0` (返回结果与查询文本完全不匹配) 和 `1` (返回结果与查询文本完全匹配) 之间的数值。您可以使用 `relevance` 属性来将不是很匹配的结果过滤移除。

In this example query for the address “515 15th St NW, Washington, DC 20004”, the expected result is first in the response with a `relevance` of `0.875`. Other results in other cities, since they don’t match the search text as closely, have a `relevance` score of `0.2`.

在这个查询示例中，查询请求的地址为 “515 15th St NW, Washington, DC 20004”，预期的结果将是回复中的第一条，它的 `relevance` 相关性数值为 `0.875`。而剩下的结果都位于其他城市，由于它们与搜索文本并不密切相关，所以 `relevance` 相关性数值显示为 `0.2`。????? 这个与实际查看的结果有出入！

```
https://api.mapbox.com/geocoding/v5/mapbox.places/515%2015th%20St%20NW%2C%20Washington%2C%20DC%2020004.json?types=address&access_token={{ <UserAccessToken /> }}
```

##### Prominence score
##### 显著普遍性分数

In the case that multiple features have the same `relevance` score, a second filter called `score` is applied. This is based on the popularity or prominence of a feature. For example, a search for “Paris” will equally match “Paris, France” and “Paris, Texas” — they’ll have the same `relevance` score. The `score` filter helps break this tie on the backend, and surfaces “Paris, France” first since it is a more popular feature:

在多个元素获得相同 `relevance` 相关性分数的情况下，我们就要使用第二个过滤器 `score`。这是一个基于元素普遍性或显著性的分数。例如，一条关于 “巴黎” 的查询将会给 “巴黎，法国” 和 “巴黎，德克萨斯” 相同的 `relevance` 相关性分数。显著普遍性 `score` 会在后端打破平衡僵局，将 “巴黎，法国” 这条结果置顶，因为这一地址特征元素更为普遍流行：

```
https://api.mapbox.com/geocoding/v5/mapbox.places/paris.json?access_token={{ <UserAccessToken /> }}
```

#### Result prioritization in reverse geocoding
#### 反向地理编码中的结果优先次序

For reverse geocodes, results at a given set of coordinates are sorted by order of **spatial hierarchy**. For example, a more granular feature such as an `address`, `poi`, or `postcode` will return first in the response before feature types like `region`  or `country`. The full spatial hierarchy, ordered from the most granular to the largest, is: _point of interest (POI)_, _address_, _neighborhood_, _locality_, _postcode_, _place_, _district_, _region_, and _country_. (For more details about these geographic information types, see the [Source data section](#source-data).)

在反向地理编码中，那些由给定坐标点返回的查询结果都会根据 **空间层级** 来排序。例如，更接近于一个具体地点的，像是 `address`, `poi` 和 `postcode` 这样的元素，将会在那些范围更广的，类似于 `region` 或者 `country` 的元素前面被返回。一个完全的空间层级会将元素显示的先后顺序，根据其覆盖范围特征由小到大，来决定，如：_point of interest (POI)_, _address_, _neighborhood_, _locality_, _postcode_, _place_, _district_, _region_ 和 _country_。（更多有关这些地理信息类别的内容，请见 [源数据](#source-data)。）

This reverse geocoding query example returns features closest to the query point (in the case of point features like `address` and `poi`) and features that contain the query point (in the case of polygon features like `place` or `region`), in order of hierarchy from the most granular (address or POI) to the largest feature (country):

这一反向地理编码示例将查询结果元素的文本信息依照自小（address 或者 POI）至大（country）的空间层级显示返回，那些最接近于查询坐标点的元素（类似于 `address` 和 `poi`）显示在前，而那些包含着坐标点的元素（类似于`place` 或者 `region`）显示在后。

```
https://api.mapbox.com/geocoding/v5/mapbox.places/-122.463%2C%2037.7648.json?access_token={{ <UserAccessToken /> }}
```

## Access Mapbox geocoding services
## 获取Mapbox Geocoding服务

You can access the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) directly, through Mapbox Studio, or using one of several wrapper libraries integrate it into applications across platforms.

您可以从 [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 直接获取 Mapbox Geocoding API 服务。您也可以通过Mapbox工作室，或者选择将一个包装库添加到跨平台应用中来间接使用服务。

### Use the Mapbox Geocoding API
### 使用Mapbox Geocoding API

You can send requests to the Mapbox Geocoding API via many Mapbox mapping tools and plugins, but you can also make calls to the API directly using your preferred HTTP client. If you would like to make calls directly, read our full [API documentation](https://docs.mapbox.com/api/search/#geocoding). If you would prefer to use one of our other tools, read on!

您可以通过Mapbox中的诸多工具和插件来向Mapbox Geocoding API发送请求，但是您也能使用自己偏好的HTTP client来直接调用API。如果您想要直接调用API，请参考我们完整的 [API 文档](https://docs.mapbox.com/api/search/#geocoding)。如果您偏好使用我们提供的其他工具，请继续阅读下文！

### Test the Geocoding API
### 测试Geocoding API服务

If you would like to get a feel for how the Mapbox Geocoding API works without building a whole application, we also provide an [API Playground](https://www.mapbox.com/search-playground/) that works similarly to the live example at the beginning of this guide. Besides providing a convenient user interface to test queries, the API playground allows you to test the API's URL and query parameters, such as autocomplete, proximity, and mode.

如果您有意在不构建一整个应用的情况下快速体验Mapbox Geocoding API，我们为您提供了与本篇指南开头所展示的实例类似的[API Playground](https://www.mapbox.com/search-playground/)。除了具备方便测试查询请求的用户界面以外，这个API Playground还允许您测试API的请求URL网址和查询参数，例如：是否自动完成，是否允许邻域偏差，以及查询模式等。

{{
<a className='link txt-ms txt-bold' href='https://www.mapbox.com/search-playground/'><ChevronousText text="Visit the Search Playground" /></a>
}}

### Geocoding in Mapbox Studio
### 在Mapbox工作室使用Geocoding服务

The [Mapbox Studio dataset editor](https://www.mapbox.com/studio/datasets) allows you to [create your own custom datasets](/help/how-mapbox-works/creating-data/) by importing data, drawing it manually, or searching for it in the **Search places** toolbar. When you search for places in the toolbar, you're using the Mapbox Geocoding API to find data to add to your custom dataset. Note that within the dataset editor you can search for and add for countries, regions, districts, postcodes, places, localities, neighborhoods, and addresses, but not POIs. 

[Mapbox工作室 数据集编辑器](https://www.mapbox.com/studio/datasets) 允许您通过导入数据，手动绘制，或者在注有 **搜索地点** 字样的工具栏搜索地点，来 [创建您的自定义数据集](/help/how-mapbox-works/creating-data/)。当您在搜索栏搜寻不同地点，您即已开始使用Mapbox Geocoding API来搜索以添加至自定义数据集中的数据。注意在数据集编辑器中，您可以搜索并添加countries, regions, districts, postcodes, places, localities, neighborhoods 和 addresses到自定义数据集，但是不能添加POIs的数据。

### Libraries and plugins
### 工具库和插件

If you would like to add a search tool to your application to find addresses, POIs, or features near your user's location, we have several wrapper libraries that allow you to integrate the Mapbox Geocoding API into your existing application seamlessly:

如果您有意在应用中添加一个搜索工具来查找您用户附近的地址，POIs，或者其他地理元素信息，我们可为您提供诸多包装库以便您将Mapbox Geocoding API无缝添加到现有应用中：

- **Web**: [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder) for Mapbox GL JS and both [geocoderControl](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocodercontrol/) and [geocoder](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocoder/) for Mapbox.js
- **Android**: [Mapbox Java SDK](https://www.mapbox.com/android-docs/java/examples/)
- **iOS**: [MapboxGeocoder.swift](https://www.github.com/mapbox/MapboxGeocoder.swift)

- **网页**: 为使用 Mapbox GL JS，我们有 [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder)；为使用 Mapbox.js，我们有 [geocoderControl](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocodercontrol/) 和 [geocoder](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocoder/)。
- **Android**: [Mapbox Java SDK](https://www.mapbox.com/android-docs/java/examples/)
- **iOS**: [MapboxGeocoder.swift](https://www.github.com/mapbox/MapboxGeocoder.swift)

In addition, we offer libraries for:

此外，我们还为Python，JavaScript和React提供了以下工具库：

- [Python](https://github.com/mapbox/mapbox-sdk-py)
- [JavaScript](https://github.com/mapbox/mapbox-sdk-js)
- [React](https://github.com/mapbox/react-geocoder)

Here's an example of the [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder) in action with the query parameter `autocomplete=true`:

下面这一动态示例为您演示了 [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder) 的自动完成功能，即 `autocomplete=true` 的时候：

<p><img src="/help/img/api/geocode.gif" alt="geocode animation" /></p>

To build a similar web application using Mapbox GL JS, explore the [Set a point after Geocoder result](https://www.mapbox.com/mapbox-gl-js/example/point-from-geocoder-result/) example.

若想使用Mapbox GL JS来构建一个类似的网页应用，请探究 [Set a point after Geocoder result 根据地理编码结果设置标记点](https://www.mapbox.com/mapbox-gl-js/example/point-from-geocoder-result/) 里面的示例。

## Providing geocoding feedback
## 为地理编码服务提供反馈意见

If you find an error, would like to provide general feedback, or want to request new features, you can use the [Geocoding Feedback tool](https://www.mapbox.com/geocoder-feedback/).

如果您在探索Mapbox地理编码服务过程中发现了错误或问题，希望提供反馈意见，或者想要请求新的功能，您可以使用 [地理编码意见反馈工具](https://www.mapbox.com/geocoder-feedback/)。
