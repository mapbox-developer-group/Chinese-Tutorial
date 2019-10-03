---
title: Make a choropleth map with the Mapbox Visual for Power BI
description: Create a choropleth data map with the Mapbox Visual for Microsoft Power BI.
thumbnail: powerBiChoroplethMap
topics:
- third party integration
level: 2
language:
- No code
prereq: Familiarity with Microsoft Power BI.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Button from '@mapbox/mr-ui/button';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

此教程将展示如何在微软Power BI(https://powerbi.microsoft.com/en-us/)中使用Mapbox Visual。我们将使用来自美国各州的自然火灾数据以及一个自定义的瓦片集来创建地区分布地图。瓦片集包含了以县为单位的美国自然火灾统计数据。地区分布图可以显示每个州和县不同的受灾程度，帮助读图人更好地从不同的尺度分析问题。您将需要一个Mapbox账户以及一个微软Power BI账户。

![A screenshot of a choropleth visualization in Power BI](/help/img/3rdparty/power-bi-choropleth-final.png)

{{
<Note
  imageComponent={<BookImage />}
>
  <p>此教程将展示如何在Power BI在线版本中使用Mapbox Visual。桌面版本的操作流程基本一致，但是界面有所区别。</p>
</Note>
}}

## 准备工作

您需要进行以下准备工作：

- **Mapbox账号**：如果要将Mapbox Visual工具添加到Power BI程序中，您将需要一个Mapbox秘钥。此秘钥可以通过[免费注册](https://account.mapbox.com/auth/signup/)获取。
- **Power BI账号**：登陆您的[Power BI账号](https://app.powerbi.com/)或者创建一个新的账号。
- **支持微软Power BI的Mapbox Visual插件**：您可以在Power BI应用中心找到并添加Mapbox Visual，或者您也可以从[Github](https://github.com/mapbox/mapboxgl-powerbi)下载[Mapbox Visual最新版本](https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz)。详情请阅读本教程。
- **地理数据**：您需要上传一个GeoJSON文件，以作为Mapbox Studio中的瓦片集。这个文件包含了县级的美国森林火灾数据。

{{
<Button href="/help/data/power-bi-wildfires-by-county.geojson" passthroughProps={{ download: "power-bi-wildfires-by-county.geojson" }} >
    <Icon name='arrow-down' inline={true} /> 下载GeoJSON文件
</Button>
}}

- **Power BI中的数据**：您需要上传下面的CSV样本数据集文件至Power BI中，这个文件中包含了美国自然火灾的历史数据。

{{
<Button href="/help/data/power-bi-2014-widfires.csv" passthroughProps={{ download: "power-bi-2014-widfires" }} >
    <Icon name='arrow-down' inline={true} /> 下载CSV文件
</Button>
}}

## 上传瓦片集至Mapbox中

在您能从Power BI报告中索引您已经下载的GeoJSON文件之前，您需要将此文件作为一个[瓦片集](/help/glossary/tileset/)上传至Mapbox中。

{{
<Note
  imageComponent={<BookImage />}
>
  <p>Mapbox只允许以下类型的文件上传为一个瓦片集：</p>
  <ul>
    <li>MBTile</li>
    <li>KML</li>
    <li>GPX</li>
    <li>GeoJSON</li>
    <li>Shapefile (压缩)</li>
    <li>CSV</li>
  </ul>
  <p>在<a href="/help/troubleshooting/uploads/#tilesets">这里</a>可以阅读更多的有关上传文件大小的限制。</p>
</Note>
}}

1. 在Mapbox Studio中找到[瓦片集页面](https://www.mapbox.com/studio/tilesets/)
2. 点击**新的瓦片集**按钮。
![Screenshot showing the New tileset button in Mapbox Studio](/help/img/3rdparty/power-bi-new-tileset.png)3. 在_新的瓦片集_窗口中，您可以点击**选择一个文件**并选择一个文件，或者您可以将您的本地文件直接拖拽到窗口中。
4. 当您看到一个提示的时候，点击**确认**。
![Screenshot showing the Confirm button in the New tileset window in Mapbox Studio](/help/img/3rdparty/power-bi-confirm-tileset-upload.png)
5. 当文件上传完毕之后，您将会看到一个完成消息。点击消息中的链接，您将可以直接打开新创建的瓦片集的信息页。这个信息页面包含了_瓦片集ID_，_图层名_，以及图层的_属性_。所有的这些信息您都可以在Power BI中索引。

您将会在[添加一个瓦片集](#add-a-custom-tileset)这一章中使用以上信息。现在，请打开Power BI。

## 在Power BI中添加数据

首先，您需要将您所下载的自然火灾数据添加到一个新的Power BI工作环境中。

1. 在Power BI中，点击**获取数据**。您将可以载入或者连接到一个数据源。
2. 在_文件_选项中，点击**获取**。
3. 选择**本地文件**以上传自然火灾CSV数据文件。

![A screenshot showing how to upload a CSV to Power BI](/help/img/3rdparty/power-bi-choropleth-upload.png)

{{
<Note
  title="Notes on using a custom dataset in Power BI"
  imageComponent={<BookImage />}
>
  <p>您的CSV文件至少需要包含2列数据。一列数据是唯一的ID，这一列ID用于匹配每一个瓦片集。另一列是具体的数据值，数据值应该与每一个瓦片相互对应和关联。（此教程所使用的数据中，`state_name`是唯一识别ID，此ID将用于在Power BI中匹配美国各州的瓦片集。每个ID之后所赋予的数据值是对应的州的烧毁面积。）</p>
</Note>
}}

## 创建一份新的报告

1. 点击**我的工作环境**并选择**数据集**标签。
2. 点击新数据集旁边的**创建一份报告**选项（柱状图图标）。您将会看到一个报告结果窗口。

![A GIF showing how to create a new report in Power BI](/help/img/3rdparty/power-bi-choropleth-new-report.gif)

## 将Mapbox Visual添加到报告中

您可以在_微软Power BI中的Mapbox Visual_中使用任何包含有地理信息的数据集。您需要以下步骤将Mapbox Visual添加到您的报告中：

1. 在_可视化_窗格中，点击**载入一个自定义可视化**选项，此图标由三个小点组成。
2. 选择**从工作环境载入**。
{{<img alt='如何从应用商店向Power BI中载入一个可视化' src='/help/img/3rdparty/power-bi-choropleth-import.png' className='block wmax600 pt18 mx-auto' />}}
3. 在搜索栏中输入“Mapbox”并回车。
4. 点击位于_Mapbox Visual_选项旁边的**添加**按钮，将一个可视化添加至您的Power BI报告中。添加完成之后，在您的_可视化_窗格中会显示一个蓝色的Mapbox图标。

{{<img alt='Power BI可视化窗格中的Mapbox Visual图标' src='/help/img/3rdparty/power-bi-choropleth-mapbox-visual.png' className='block wmax600 mx-auto' />}}

{{
<Note
  title="Alternative workflow: Manual upload"
  imageComponent={<BookImage />}
>
  <p>您也可以下从<a href='https://github.com/mapbox/mapboxgl-powerbi'>Mapbox</a>下载<a href='https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz'>最新版本的Mapbox Visual</a>。:</p>
  <ol>
  <li>点击<strong>载入一个自定义可视化工具</strong>图标（图标为三个小点）然后选择<strong>从文件导入</strong>。</li>
  <li>上传您刚才下载的<a href='https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz'>Mapbox Visual最新版文件</a>。</li>
  <li>一个蓝色的Mapbox图标将会在<em>可视化</em>窗格中显现。</li>
  </ol>
</Note>
}}

## 创建地区分类可视化

### 提供一个Mapbox秘钥

1. 选择_可视化_窗格中的Mapbox图标，添加一个新的可视化至您的报告中。
2. 在**字段**标签中，将数据中`state_name`拖拽至_位置_栏中。Mapbox容器可视化会提供如何创建您的第一个可视化的后续步骤。
{{<img alt='state_name已经被添加到位置栏中' src='/help/img/3rdparty/power-bi-choropleth-state-name.png' className='mx-auto mt18' />}}
3. 通过您的秘钥连接Mapbox账号：
    - 点击可视化容器中的**点击此处已获得一个免费的Mapbox秘钥**链接。如有提示，请允许访问外部链接。您将会被转移到Mapbox登录界面或者您的账户信息页面。
    - 在账户信息页面(https://www.mapbox.com/account/access-tokens)复制您的Mapbox秘钥。
4. 返回Power BI界面，选择**格式**标签以打开**可视化设置**选项。在_秘钥_字段中粘贴您的秘钥。

{{<img alt='在Power BI中添加Mapbox秘钥' src='/help/img/3rdparty/power-bi-choropleth-access-token.gif' className='block wmax600 mx-auto' />}}

### 创建地区分布图

1. 在**可视化设置**窗格中，将_地图风格_设置为_暗黑_。
2. 将数据集中的`ACRES`字段拖拽至_颜色_栏目中。
3. 返回**格式**标签，关闭**圆圈**选项，打开**地区分布**选项。

您将可以看到一个地区分布图。此图展示了美国各州的受灾面积统计情况。

![Screenshot showing the choropleth visualization in Power BI](/help/img/3rdparty/power-bi-choropleth-visualization-on.png)

### 添加一个瓦片集

如果想要展示更加详细的美国自然火灾数据，您需要将之前您所创建的县级瓦片集信息与您的可视化关联起来。

为了能够将县级信息添加到Power BI中，您需要将它们的ID与Power BI中对应的字段关联起来。您需要的信息有_瓦片集ID_、_图层名_以及_唯一属性名_。

![将瓦片集添加到Power BI时所需要的信息：瓦片集ID、图层名以及属性名](/help/img/3rdparty/power-bi-tileset-details-pt2.png)

1. 在**格式**标签中，点击**地区分布图**打开一个地区分布图层的设置窗口。
2. 在_等级数_下拉菜单中选择`2`。（设置两个等级是为了能够将州级设置为1，将您将要添加的县级数据设置为2。）
3. 在_等级_下拉菜单中选择`2`。
4. 点击_数据等级2_下拉菜单。
5. 选择_自定义瓦片集_选项。
{{<img alt='如何向Power BI中的地区分布图添加一个自定义的瓦片集' src='/help/img/3rdparty/power-bi-choropleth-custom-tileset.png' className='mx-auto mt18' />}}
6. 在_等级2矢量瓦片URL_字段中，输入瓦片集的ID。这个字段中的瓦片集ID必须以`mapbox://`开头。
7. 在_等级2源图层名_字段中，输入图层名。
8. 在_等级2矢量属性_字段中，输入唯一识别的属性名：`id`。
9. 再次点击**字段**标签。将数据选项中的`county_id`字段拖拽至_位置_栏中。

{{
<AppropriateImage imageId="powerBiAddCustomTileset" alt="如何向Power BI添加Mapbox瓦片集ID、图层名以及属性名" />
}}

{{
<Note
  title="在Power BI中使用自定义的瓦片集"
  imageComponent={<BookImage />}
>
  <p>瓦片集的边界必须包含一个唯一识别的属性列，这个属性列将用于与Power BI中的数据集做匹配。常用的有：FIPS码、邮编、ISO码或者任何的唯一字符串。</p>
</Note>
}}

## 最终成果

使用位于可视化窗口左上角的按钮实现在州和县级数据之间的切换。将鼠标停在一个州或者县区域可以显示此地区的受灾统计面积。

![图为Power BI中一个县级的地区分布可视化](/help/img/3rdparty/power-bi-choropleth-counties.png)

至此，您已经使用微软Power BI中的Mapbox Visual创建了一个地区分布可视化。

## 下一步

您可以尝试更多的自定义地区分布可视化的方法。例如，您可以使用在**格式**标签中的**地区分布**设置以改变可视化的色彩设计。

请前往[Github](https://github.com/mapbox/mapboxgl-powerbi)或者[客服](https://www.mapbox.com/contact/support/#other)寻求更多的帮助。

想要学习更多的有关Mapbox和Power BI的知识吗？请移步此处以探索更多的可能性，包括

想要更加深入的学习Mapbox和Power BI吗？[在这里](https://www.mapbox.com/contact/sales)您可以了解到更多的可能性，包括通过添加自定义的shapefile文件来可视化领土范围、添加详细的室内地图，或者是大型点集数据的可视化。
