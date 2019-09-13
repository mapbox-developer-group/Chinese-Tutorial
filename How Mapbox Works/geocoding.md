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

[Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 主要执行两项任务：*地理编码* 和 *反向地理编码*。地理编码可以将地址文本转换成对应的地理坐标，例如，将 `2 Lincoln Memorial Circle NW` 转换为 `-77.050,38.889`。反向地理编码则是指将地理坐标转化为地址文本说明的过程，例如，将 `-77.050,38.889` 转化为 `2 Lincoln Memorial Circle NW`。

All geocoding requests require you to submit a *query*, or what you're trying to find. When you make a query, you get a *response*, a JSON-formatted document of the most relevant results from your query. This guide provides an overview of how the Geocoding API works, how to use it, how to provide feedback, and links to relevant documentation to get you started.

所有的地理编码请求都需要您提交一个 *查询* 问题，换言之，您需要告诉API您想查找的地点。当您发出一个查询请求，您将获得一则 *回复* 信息。这则 *回复* 记录了与您提出的查询请求最相关的查询结果，它以JSON文件格式出现。本篇指南将为您介绍：Geocoding API如何
，如何使用Geocoding API，以及如何提交相关的反馈意见给Mapbox。您可以参考本篇指南最后的相关文档来开始使用Mapbox地理编码服务。

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-geocoding-works.html" />
}}

Here's an example that uses the [Mapbox GL geocoder plugin](https://github.com/mapbox/mapbox-gl-geocoder) to add forward geocoding to a web app built with Mapbox GL JS. Type in a location to view the raw JSON response for that query. Geocoding results are returned in [Carmen GeoJSON](https://github.com/mapbox/carmen/blob/master/carmen-geojson.md) format and contain both descriptive location information and geographic information. You can use the geographic information returned in the JSON response to show your query on a map, like in this example, or do additional spatial analysis.

本示例使用了 [Mapbox GL geocoder 插件](https://github.com/mapbox/mapbox-gl-geocoder) 将地理编码功能添加到了一个由Mapbox GL JS创建的网页应用中。输入一个地址，您便可以在地图下方查看本次查询所返回的原始JSON代码回复信息。地理编码查询结果会以 [Carmen GeoJSON](https://github.com/mapbox/carmen/blob/master/carmen-geojson.md) 的格式返回，它既包含了描述性位置信息，又包含了地理信息。您可利用JSON回复中的地理信息，将您的查询请求及结果显示在地图上，正如本示例所展示的那样。此外，您还可以利用所返回的地理信息进行额外的空间分析。

## How geocoding works
## 地理编码如何运作

The [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) has two distinct parts: the **source data** we use to define locations and the **tools** we use to search for and return those locations.

[Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 有两个截然不同的组成部分：一个是我们用来定义地点位置的源数据，另一个是我们用来搜索并返回地点坐标的工具箱。

### Source data
### 源数据

The Mapbox Geocoding API contains [data sources](https://www.mapbox.com/about/maps/#data-sources) from governments, open data projects, and private companies. In some cases, results from the Geocoding API may differ from [Mapbox Streets](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/) or OpenStreetMap data.

Mapbox Geocoding API 包含了来自政府机构，开源数据项目及私营公司的[源数据](https://www.mapbox.com/about/maps/#data-sources). 在某些情况下，Geocoding API 返回的查询结果与 [Mapbox Streets](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/) 或者 OpenStreetMap 数据不一致。

The Mapbox Geocoding API source data contains the following types of geographic information, ordered from the most granular to the largest:

Mapbox Geocoding API 源数据包含了以下几种地理信息（顺序排列根据覆盖区域自点到面，由小至大）：

- **Points of interest (POI):** A named place including commercial businesses, public buildings, monuments, and parks, among other features.
- **Address:** A specific mailing address, including the address number if applicable.
- **Neighborhood:** A colloquial name for a smaller area within a place. Neighborhoods do not necessarily have specific, legally defined boundaries. Only present in some countries.
- **Locality:** An administrative unit that is smaller than a place. Only present in some countries.
- **Postcode:** A geographic area of the address component used for sorting mail.
- **Place:** Cities, towns, and villages. Note that some large cities (such as Tokyo and Istanbul) may be categorized as regions rather than places.
- **District:** An administrative unit that is larger than a place but smaller than a region. Only present in some countries.
- **Region:** States, provinces, and prefectures. This is typically the largest sub-national administrative unit of a country. Note that some large cities (such as Tokyo and Istanbul) may be categorized as regions rather than places.
- **Country:** Generally recognized countries or, in some cases like Hong Kong, an area of quasi-national administrative status that has been given a designated country code under ISO 3166-1.

- **兴趣点（POI, Points of Interest）：** 一个有名称的地点，它可以是在其余地理信息要素中的商务楼，公共建筑，纪念碑/历史遗迹，公园。
- **地址：** 一个具体的邮寄地址，包含门牌号或建筑物号码（如果适用）。
- **街区：** 一个地方子区域的俗称。街区不一定有确切的，法定的边界。仅于某些国家地址中出现。
- **本地居民区：** 一个小于地方的行政区域单位。仅于某些国家地址中出现。
- **邮政行政区（以邮编代表）：** （邮编）作为地址中的一部分，描述用来分理邮件的地理区域。
- **地方：** 以城市或村镇为代表。请注意，一些大城市（例如，东京和伊斯坦布尔）可被归类为区域而不是地方。
- **区级行政区：** 一个比地方大，同时又比区域小的行政区域单位。仅于某些国家地址中出现。
- **区域：** 以州，省和县为代表。通常它是一个仅次于国家的最大行政区域单位。值得注意的是，一些大城市（例如，东京和伊斯坦布尔）可被归类为区域而不是地方。
- **国家或地区：** 一般指公认的国家，或者一些情况下也指地区， 如：香港特别行政区。它们都有指定的 ISO 3166-1 国家或地区编码。

This hierarchy of feature types is also used to determine what will be returned as the encompassing parent features in a Geocoding API response object's [`context` 属性](https://docs.mapbox.com/api/search/#geocoding-response-object). For example, if the returned feature is a `place` (like Detroit), then the encompassing parent features in the `context` property will be the `region` (the state of Michigan) and the `country` (United States).

这个关于要素类别的层次结构也可以被用来决定一个 Geocoding API 的JSON回复对象中 [`context` 属性](https://docs.mapbox.com/api/search/#geocoding-response-object) 所包含的父要素。举个例子，如果返回的要素是一个 `地方` （如：底特律），那么其 `context` 属性将会是 `区域` （密歇根州） 和  `国家或地区` (美国)。


### Tools
### 工具

The Mapbox Geocoding API uses [Carmen](https://github.com/mapbox/carmen), an open source project for Mapnik vector tile-based geocoding. For more on Carmen, see [How does Carmen work?](https://github.com/mapbox/carmen#how-does-carmen-work).

Mapbox Geocoding API 使用 [Carmen](https://github.com/mapbox/carmen)，一个为Mapnik矢量切片进行地理编码的开源项目。若想了解跟多有关Carmen的内容，您可以参考 [Carmen是如何运作的？](https://github.com/mapbox/carmen#how-does-carmen-work)。

### Customizing your queries

The Mapbox Geocoding API accepts many optional parameters. You can use these optional parameters to customize your queries so that the most relevant results are returned. These parameters can be specified using URL query parameters, or they can be specified as options with one of our client-side libraries or plugins. These parameters allow you to view results as you type, filter results by geographic feature type, and limit or bias results to a specified area. For example, to limit your search results to addresses in the Washington DC Metro area, you could set the `type` parameter to `address` and the `bbox` parameter to `-77.08,38.90,-76.99,38.95`. With those parameters set, your query for `Constitution Ave` will only return street addresses in the DC Metro area, and will not include features you're not interested in (like `Constitution Ave, El Paso, Texas 79908, United States`).

Read the [Geocoding API documentation](https://docs.mapbox.com/api/search/#geocoding) for more information on available features.

### Language support

The Mapbox Geocoding API accepts a `language` query parameter, which allows you to specify the language in which you would like to search. One or more languages can be specified using [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). Translation availability varies by language and region, and you can expect more consistent results for areas where the specified language is most widely used. Language support has three different levels:

- **Global coverage.** These languages are almost always present for `country`, `region`, and prominent `place` features.
- **Local coverage.** These languages may lack global coverage, but they are almost always present for `country`, `region`, and prominent `place` features where they are widely used.
- **Limited coverage.** These languages are sometimes present, but coverage tends to be inconsistent or geographically constrained.

For a current list of the languages covered at each level, see the [Geocoding API documentation](https://docs.mapbox.com/api/search/#language-coverage).

### Search result prioritization

Results from geocoding queries are prioritized differently depending on whether the request was a _forward geocode_ or a _reverse geocode_.

#### Result prioritization in forward geocoding

When a forward geocoding query (human-readable text like “San Francisco”) is submitted to the Mapbox Geocoding API, the geocoder uses Carmen, a text search engine, to search our spatial indexes for features that match the user’s query. (For a more detailed description of how the Carmen text search engine works, read the [Carmen documentation](https://github.com/mapbox/carmen/blob/master/docs/how-carmen-works.md).) The geocoder applies filters on the backend to sort the results that match, or partially match, the searched text. These filters are _textual relevance_ and _prominence score_.

##### Textual relevance

When the geocoder sorts and prioritizes results, the first filter that is applied is `relevance`. `relevance` is a value that indicates how well a feature in our dataset matches the query. This property is surfaced in the Geocoding API response, and is a numerical score from `0` (the result does not match the queried text at all) to `1` (the result matches the queried text most completely). You can use the `relevance` property to remove results that don't fully match the query.

In this example query for the address “515 15th St NW, Washington, DC 20004”, the expected result is first in the response with a `relevance` of `0.875`. Other results in other cities, since they don’t match the search text as closely, have a `relevance` score of `0.2`.

```
https://api.mapbox.com/geocoding/v5/mapbox.places/515%2015th%20St%20NW%2C%20Washington%2C%20DC%2020004.json?types=address&access_token={{ <UserAccessToken /> }}
```

##### Prominence score

In the case that multiple features have the same `relevance` score, a second filter called `score` is applied. This is based on the popularity or prominence of a feature. For example, a search for “Paris” will equally match “Paris, France” and “Paris, Texas” — they’ll have the same `relevance` score. The `score` filter helps break this tie on the backend, and surfaces “Paris, France” first since it is a more popular feature:

```
https://api.mapbox.com/geocoding/v5/mapbox.places/paris.json?access_token={{ <UserAccessToken /> }}
```

#### Result prioritization in reverse geocoding

For reverse geocodes, results at a given set of coordinates are sorted by order of **spatial hierarchy**. For example, a more granular feature such as an `address`, `poi`, or `postcode` will return first in the response before feature types like `region`  or `country`. The full spatial hierarchy, ordered from the most granular to the largest, is: _point of interest (POI)_, _address_, _neighborhood_, _locality_, _postcode_, _place_, _district_, _region_, and _country_. (For more details about these geographic information types, see the [Source data section](#source-data).)

This reverse geocoding query example returns features closest to the query point (in the case of point features like `address` and `poi`) and features that contain the query point (in the case of polygon features like `place` or `region`), in order of hierarchy from the most granular (address or POI) to the largest feature (country):

```
https://api.mapbox.com/geocoding/v5/mapbox.places/-122.463%2C%2037.7648.json?access_token={{ <UserAccessToken /> }}
```

## Access Mapbox geocoding services

You can access the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) directly, through Mapbox Studio, or using one of several wrapper libraries integrate it into applications across platforms.

### Use the Mapbox Geocoding API

You can send requests to the Mapbox Geocoding API via many Mapbox mapping tools and plugins, but you can also make calls to the API directly using your preferred HTTP client. If you would like to make calls directly, read our full [API documentation](https://docs.mapbox.com/api/search/#geocoding). If you would prefer to use one of our other tools, read on!

### Test the Geocoding API

If you would like to get a feel for how the Mapbox Geocoding API works without building a whole application, we also provide an [API Playground](https://www.mapbox.com/search-playground/) that works similarly to the live example at the beginning of this guide. Besides providing a convenient user interface to test queries, the API playground allows you to test the API's URL and query parameters, such as autocomplete, proximity, and mode.

{{
<a className='link txt-ms txt-bold' href='https://www.mapbox.com/search-playground/'><ChevronousText text="Visit the Search Playground" /></a>
}}

### Geocoding in Mapbox Studio

The [Mapbox Studio dataset editor](https://www.mapbox.com/studio/datasets) allows you to [create your own custom datasets](/help/how-mapbox-works/creating-data/) by importing data, drawing it manually, or searching for it in the **Search places** toolbar. When you search for places in the toolbar, you're using the Mapbox Geocoding API to find data to add to your custom dataset. Note that within the dataset editor you can search for and add for countries, regions, districts, postcodes, places, localities, neighborhoods, and addresses, but not POIs.

### Libraries and plugins

If you would like to add a search tool to your application to find addresses, POIs, or features near your user's location, we have several wrapper libraries that allow you to integrate the Mapbox Geocoding API into your existing application seamlessly:

- **Web**: [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder) for Mapbox GL JS and both [geocoderControl](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocodercontrol/) and [geocoder](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocoder/) for Mapbox.js
- **Android**: [Mapbox Java SDK](https://www.mapbox.com/android-docs/java/examples/)
- **iOS**: [MapboxGeocoder.swift](https://www.github.com/mapbox/MapboxGeocoder.swift)

In addition, we offer libraries for:

- [Python](https://github.com/mapbox/mapbox-sdk-py)
- [JavaScript](https://github.com/mapbox/mapbox-sdk-js)
- [React](https://github.com/mapbox/react-geocoder)

Here's an example of the [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder) in action with the query parameter `autocomplete=true`:

<p><img src="/help/img/api/geocode.gif" alt="geocode animation" /></p>

To build a similar web application using Mapbox GL JS, explore the [Set a point after Geocoder result](https://www.mapbox.com/mapbox-gl-js/example/point-from-geocoder-result/) example.

## Providing geocoding feedback

If you find an error, would like to provide general feedback, or want to request new features, you can use the [Geocoding Feedback tool](https://www.mapbox.com/geocoder-feedback/).
