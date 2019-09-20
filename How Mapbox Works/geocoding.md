---
标题: 地理编码
描述: 学习地理编码工作原理以及如何在您的下一个Mapbox项目中使用地理编码。
图像: /img/narrative/geocoding.svg
主题:
  - 地理编码
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import ChevronousText from '@mapbox/mr-ui/chevronous-text';"
  - "import UserAccessToken from '../../components/user-access-token';"
文章类别: 指南教程
---

[Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 主要执行两大任务：*正向地理编码* 和 *反向地理编码*。正向地理编码将地址文本转换成相应的地理坐标，例如，将 `2 Lincoln Memorial Circle NW` 转换为 `-77.050,38.889`。反向地理编码则是指将地理坐标转化为地址文本说明的过程，例如，将 `-77.050,38.889` 转化为 `2 Lincoln Memorial Circle NW`。


所有的地理编码请求都需要您提交一个 *查询* 请求，换言之，您需要告诉API您即将查找的地点。当您发出一个查询请求，您将获得一则以JSON文件格式出现的 *回复* 信息。这则 *回复* 记录了与查询请求最相关的查询结果。本篇指南将为您介绍：Geocoding API如何运作，如何使用Geocoding API，以及如何提交相关的反馈意见给Mapbox。您可以参考本篇指南最后的相关文档来开始使用Mapbox地理编码服务。

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-geocoding-works.html" />
}}


本示例使用了 [Mapbox GL geocoder 插件](https://github.com/mapbox/mapbox-gl-geocoder) 将正向地理编码功能添加到了一个由Mapbox GL JS创建的网页应用中。输入一个地址，您便可以在地图下方查看本次查询所返回的原始JSON代码回复信息。地理编码查询结果会以 [Carmen GeoJSON](https://github.com/mapbox/carmen/blob/master/carmen-geojson.md) 的格式返回，它既包含了描述性位置信息，又包含了地理信息。您可利用JSON回复中的地理信息，将查询请求及结果显示在地图上，正如本示例所展示的那样。您还可以利用所返回的地理信息另外进行空间分析。

## 地理编码如何运作

[Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 有两个截然不同的组成部分：一个是我们用来定义地点位置的 **源数据**，另一个是我们用来搜索并返回地点信息的 **工具**。

### 源数据

Mapbox Geocoding API 包含了来自政府机构，开源数据项目及私营公司的 [源数据](https://www.mapbox.com/about/maps/#data-sources)。在某些情况下，Geocoding API 返回的查询结果与 [Mapbox Streets](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/) 或者 OpenStreetMap 数据不太一致。


Mapbox Geocoding API 源数据包含了以下几种地理信息（排列顺序根据元素特征自点到面，由小至大）：

- **兴趣点 POI（Points of Interest）：** 一个有名称的地点，它可以是包含在其余地理信息要素中的商务楼，公共建筑，纪念碑/历史遗迹和公园。
- **地址 Address：** 一个具体的邮寄地址，包含门牌号或建筑物号码（如果适用）。
- **街区 Neighborhood：** 一个地方子区域的俗称。街区不一定有确切、法定的边界。仅于某些国家或地区的地址中出现。
- **本地居民区 Locality：** 一个小于地方的行政区域单位。仅于某些国家或地区的地址中出现。
- **邮政行政区（以邮编代表）Postcode：** （邮编）作为地址中的一部分，描述用来分理邮件的地理区域。
- **地方 Place：** 以城市或村镇为代表。请注意，一些大城市（例如，东京和伊斯坦布尔）可被归类为区域而不是地方。
- **区级行政区 District：** 一个比地方大，同时又比区域小的行政区域单位。仅于某些国家或地区的地址中出现。
- **区域 Region：** 以州，省和县为代表。通常它是一个仅次于国家的最大行政区域单位。值得注意的是，一些大城市（例如，东京和伊斯坦布尔）可被归类为区域而不是地方。
- **国家或地区 Country：** 一般指公认的国家，或者一些情况下也指地区， 如：香港特别行政区。它们都有指定的 ISO 3166-1 国家或地区编码。


这个有关要素类别的层级结构也可以被用来决定一个 Geocoding API JSON回复对象中 [`context` 属性](https://docs.mapbox.com/api/search/#geocoding-response-object) 所包含的父要素。举个例子，如果返回的要素是一个 `place` （如：底特律），那么其 `context` 属性将会是 `region` （密歇根州） 和  `country` (美国)。

### 工具

Mapbox Geocoding API 使用 [Carmen](https://github.com/mapbox/carmen)，它一个为基于Mapnik矢量切片的地理编码发起的开源项目。更多有关Carmen的内容，请见 [Carmen是如何运作的？](https://github.com/mapbox/carmen#how-does-carmen-work)。

### 自定义您的查询请求

Mapbox Geocoding API 接受多种可选参数。您可以使用这些可选参数来自定义您的查询请求以便返回最相关的查询结果。这些参数可以根据URL中的查询参数来指定，也可以根据任意一个我们客户端库或者插件中的选项来指定。这些参数允许您边输入边查看相关查询结果，根据地理元素类来筛选结果，以及将结果限定在指定地区。例如，若您想将搜索查询结果限制在华盛顿特区都市区内，您可以首先将 `type` 参数设为 `address`, `bbox` 参数设为`-77.08,38.90,-76.99,38.95`。有了这些参数设置，您的输入查询地点 `Constitution Ave` 将会返回限定在华盛顿特区都市区内的相关街道地址，它们并不会包含您不感兴趣的地理元素（如，位于德克萨斯州的 `Constitution Ave`， `Constitution Ave, El Paso, Texas 79908, United States）。


阅读 [Geocoding API 文档](https://docs.mapbox.com/api/search/#geocoding) 来详细了解更多 Geocoding API 的功能特征。

### 语言支持

Mapbox Geocoding API 接受一个 `language` 语言查询参数，它允许您指定用来查询搜索的语言。一种或多种语言可以根据 [ISO 639-1 代码](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 来指定。翻译的可用性因语言种类和地区而异，您可以期待从那些指定语言使用广泛的地区中获得更加一致的查询结果。语言支持有三个级别：

- **全球覆盖：** 这些语言通常都能显示并支持定义 `country`, `region`, 和显著常见的 `place` 这类元素。
- **局部覆盖：** 这些语言尽管没有覆盖全球范围，但是它们通常也可以在广泛使用这些语言的地区显示并支持定义 `country`, `region`, 和显著常见的 `place` 这类元素。
- **有限覆盖：** 这些语言有时会显示，但是其覆盖范围趋于不一致或者受到地理位置限制。


若您有兴趣了解Mapbox Geocoding API有关不同级别语言覆盖范围的最新信息，请见 [Geocoding API 文档](https://docs.mapbox.com/api/search/#language-coverage)。 


### 查询结果优先次序

根据查询请求是否为_forward geocode_ 或 _reverse geocode_，Mapbox Geocoding API会以不同的方式来决定地理编码查询服务结果的优先次序。

#### 正向地理编码中的结果优先次序

当一个正向地理编码请求被提交至 Mapbox Geocoding API （例如，可读的文本请求 “旧金山”），地理编码器将使用Carmen， 一个文本搜索引擎，来搜索与用户请求相匹配的元素所对应的空间索引（想了解更多Carmen文本搜索引擎如何工作的相关内容，请阅读 [Carmen 文档](https://github.com/mapbox/carmen/blob/master/docs/how-carmen-works.md)）。地理编码器将在后端使用过滤器来将与搜索文本匹配的或部分匹配的结果进行排序。这些过滤器包括_textual relevance 文本相关性_ 和 _prominence score 显著普遍性分数_。

##### 文本相关性

当地理编码器对查询结果进行排序并决定显示的优先次序时，第一个使用的过滤器是 `relevance`，相关性。 `relevance` 是一个可以表示数据集中元素与查询文本匹配程度的数值。这一属性在Geocoding API的回复结果中就有所体现，它是一个介于 `0` (返回结果与查询文本完全不匹配) 和 `1` (返回结果与查询文本完全匹配) 之间的数值。您可以使用 `relevance` 属性来将不是很匹配的结果过滤移除。

在这个查询示例中，查询请求的地址为 “515 15th St NW, Washington, DC 20004”，预期的结果将是回复中的第一条，它的 `relevance` 相关性数值为 `0.875`。而剩下的结果都位于其他城市，由于它们与搜索文本并不密切相关，所以 `relevance` 相关性数值显示为 `0.2`。

```
https://api.mapbox.com/geocoding/v5/mapbox.places/515%2015th%20St%20NW%2C%20Washington%2C%20DC%2020004.json?types=address&access_token={{ <UserAccessToken /> }}
```

##### 显著普遍性分数

在多个元素 `relevance` 相关性分数相同的情况下，我们就要使用第二个过滤器 `score`。这是一个基于元素普遍性或显著性的分数。例如，一条关于 “巴黎” 的查询将会给 “巴黎，法国” 和 “巴黎，德克萨斯” 相同的 `relevance` 相关性分数。显著普遍性 `score` 会在后端打破平衡僵局，将 “巴黎，法国” 这条结果置顶，因为这一地址特征元素更为普遍流行：

```
https://api.mapbox.com/geocoding/v5/mapbox.places/paris.json?access_token={{ <UserAccessToken /> }}
```

#### 反向地理编码中的结果优先次序

在反向地理编码中，那些由给定坐标点返回的查询结果都会根据 **空间层级** 来排序。例如，更接近于一个具体地点的，像是 `address`, `poi` 和 `postcode` 这样的元素，将会在那些范围更广的，类似于 `region` 或者 `country` 的元素前面被返回。一个完全的空间层级会将元素显示的先后顺序，根据其覆盖范围特征由小到大，来决定，如：_point of interest (POI)_, _address_, _neighborhood_, _locality_, _postcode_, _place_, _district_, _region_ 和 _country_。（更多有关这些地理信息类别的内容，请见 [源数据](#source-data)。）

这一反向地理编码示例将查询结果元素的文本信息依照自小（address 或者 POI）至大（country）的空间层级显示返回，那些最接近于查询坐标点的元素（类似于 `address` 和 `poi`）显示在前，而那些包含着坐标点的元素（类似于`place` 或者 `region`）显示在后。

```
https://api.mapbox.com/geocoding/v5/mapbox.places/-122.463%2C%2037.7648.json?access_token={{ <UserAccessToken /> }}
```

## 获取Mapbox Geocoding服务

您可以从 [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) 直接获取 Mapbox Geocoding API 服务。您也可以通过Mapbox工作室，或者选择将一个包装库添加到跨平台应用中来间接使用服务。

### 使用Mapbox Geocoding API

您可以通过Mapbox中的诸多工具和插件来向Mapbox Geocoding API发送请求，但是您也能使用自己偏好的HTTP client来直接调用API。如果您想要直接调用API，请参考我们完整的 [API 文档](https://docs.mapbox.com/api/search/#geocoding)。如果您偏好使用我们提供的其他工具，请继续阅读下文！

### 测试Geocoding API服务

如果您有意在不构建一整个应用的情况下快速体验Mapbox Geocoding API，我们为您提供了与本篇指南开头所展示的实例类似的[API Playground](https://www.mapbox.com/search-playground/)。除了具备方便测试查询请求的用户界面以外，这个API Playground还允许您测试API的请求URL网址和查询参数，例如：是否自动完成，是否允许邻域偏差，以及查询模式等。

{{
<a className='link txt-ms txt-bold' href='https://www.mapbox.com/search-playground/'><ChevronousText text="Visit the Search Playground" /></a>
}}


### 在Mapbox工作室使用Geocoding服务

[Mapbox工作室 数据集编辑器](https://www.mapbox.com/studio/datasets) 允许您通过导入数据，手动绘制，或者在注有 **搜索地点** 字样的工具栏搜索地点，来 [创建您的自定义数据集](/help/how-mapbox-works/creating-data/)。当您在搜索栏搜寻不同地点，您即已开始使用Mapbox Geocoding API来搜索以添加至自定义数据集中的数据。注意在数据集编辑器中，您可以搜索并添加countries, regions, districts, postcodes, places, localities, neighborhoods 和 addresses到自定义数据集，但是不能添加POIs的数据。

### 工具库和插件

如果您有意在应用中添加一个搜索工具来查找您用户附近的地址，POIs，或者其他地理元素信息，我们可为您提供诸多包装库以便您将Mapbox Geocoding API无缝添加到现有应用中：

- **网页**: 为使用 Mapbox GL JS，我们有 [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder)；为使用 Mapbox.js，我们有 [geocoderControl](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocodercontrol/) 和 [geocoder](https://www.mapbox.com/mapbox.js/api/v3.0.1/l-mapbox-geocoder/)。
- **Android**: [Mapbox Java SDK](https://www.mapbox.com/android-docs/java/examples/)
- **iOS**: [MapboxGeocoder.swift](https://www.github.com/mapbox/MapboxGeocoder.swift)

此外，我们还为Python，JavaScript和React提供了以下工具库：

- [Python](https://github.com/mapbox/mapbox-sdk-py)
- [JavaScript](https://github.com/mapbox/mapbox-sdk-js)
- [React](https://github.com/mapbox/react-geocoder)


下面这一动态示例为您演示了 [Mapbox GL Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder) 的自动完成功能，即 `autocomplete=true` 的时候：

<p><img src="/help/img/api/geocode.gif" alt="geocode animation" /></p>

若想使用Mapbox GL JS来构建一个类似的网页应用，请探究 [Set a point after Geocoder result 根据地理编码结果设置标记点](https://www.mapbox.com/mapbox-gl-js/example/point-from-geocoder-result/) 里面的示例。

## 为地理编码服务提供反馈意见

如果您在探索Mapbox地理编码服务过程中发现了错误或问题，希望提供反馈意见，或者想要请求新的功能，您可以使用 [地理编码意见反馈工具](https://www.mapbox.com/geocoder-feedback/)。
