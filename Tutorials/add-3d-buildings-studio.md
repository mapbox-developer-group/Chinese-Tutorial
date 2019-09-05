---
题目: 将3D建筑添加到Mapbox工作空间样式
描述: 在Mapbox Studio中，添加3D建筑物图层到一个地图样式中。
thumbnail: add3dBuildingsStudio
主题:
- 地图设计
等级: 1
语言:
- 无编码
前置Js:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { Video } from '../../components/video';"
  - "import ChangePitch from '../../video/add-3d-buildings-studio-change-pitch.mp4';"
内容类型: 教程
---

本教程将指导使用Mapbox工作空间，向地图样式中添加三维建筑图层，

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjj0b5ie80ec32so5uo8ox21m.html?fresh=true&access_token=MapboxAccessToken#15/40.751589/-73.986485/-28/60" />
}}

## 准备

在开始本教程之前，需要在 [Mapbox账号中心](https://account.mapbox.com) 创建一个Mapbox账号。

## 创建一个新样式

首先，你需要在Mapbox工作空间里创建一个新的地图样式

1. 登录到您的Mapbox帐户并导航到 [样式](https://studio.mapbox.com/styles)页面。
2. 点击**新样式**按钮。找到_基本模板_样式，然后单击**自定义基本模板**。
3. 在Mapbox工作室样式编辑器中，重命名此新样式，以便日后查找。单击屏幕左上角的标题字段，并将标题更改为“3D建筑物”。
4. 在右上角的搜索栏中，输入“帝国大厦”并选择第一个结果。

{{
<AppropriateImage 
  imageId="add3dBuildingsStudioLocationSearch"
  alt="Screenshot showing a new map view in Mapbox Studio"
/>
}}

地图视图将会以纽约帝国大厦为中心进行移动。

## 编辑建筑物图层

接下来，你将会编辑样式中的建筑物图层
<!--copyeditor ignore okay-->
1. 在屏幕左侧的图层面板中，选择**建筑物**图层。
2. 点击**选择数据**。它可以打开x射线视图，显示来自建筑层的数据
3. 单击“新建图层”面板中的**类型**选项，然后选择“填充拉伸”选项。如果系统提示您这样做，请单击**确定**。
4. 移除此层上显示的所有过滤器。
5. 单击 **+创建过滤器** 并选择**压缩**数据属性。
6. 将下拉菜单设置为任意，然后单击**空**按钮。
7.  选择 **true**。
8. 点击**样式**选项，返回建筑物图层的样式面板。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioEditFilter"
    alt="Screenshot showing how to edit a layer filter in Mapbox Studio"
  />
}}

现在建筑图层的类型已经更改，还需要调整其样式设置以显示所需的3D效果。

{{ <Note imageComponent={<BookImage />}> }}
本教程利用了地图框街道v7中的建筑层。如果您有想要在地图样式中使用的自定义建筑数据，则可以使用“Mapbox 工作空间 ”或“地图框上传”应用编程接口将这些数据作为一个地形设置上传到“地图框”。{{ }}
{{ </Note> }}

## 调整页面样式设置

接下来，你将会通过调整图层高度和基础高度属性来完成想要的3D效果。

### 设置高度属性

1. 选择建筑物图层并点击**高度**属性。
2. 选择**跨数据范围样式**选项。
3. 在 _选择数字数据字段_ 面板中，单击**高度**。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioStyleHeight"
    alt="Screenshot showing the style across data range option in Mapbox Studio"
  />
}}

4. 第一部分是已经设置为高度0和填充高度0。保持这些设置不变。
5. 在第二部分，保持高度设置为`999`，并将填充高度选项更改为`999`。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioStyleMaxHeight"
    alt="Screenshot showing the style max height option in Mapbox Studio"
  />
}}

### 设置基础高度属性

图层的基本高度属性也需要调整。这将处理任何的建筑物情况，这些建筑物具有基础高度和使其成为形状不同的独立高度。如果不设置基础高度属性，建筑物将失去一些细微的建筑特征。

1. 选择 _建筑物_ 图层，然后点击**基础高度**。
2. 选择**跨数据范围样式**选项。
3. 在 _选择数字数据字段_ 面板中，选择**最小高度**。
4. 第一个部分已经设置为高度0和填充基础高度0。保持这些设置不变。
5. 在第二个部分，保持 _高度_ 设置为`999`，并将  _填充基础高度 _ 选项更改为`999`。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioFillBaseHeight"
    alt="Screenshot showing how to adjust the base height setting in Mapbox Studio"
  />
}}

### 突出显示图层

由于建筑图层在图层列表中的上方有许多项目，因此这些项目以此方式呈现在建筑物的顶部。要使建筑物更加突出，可以将建筑图层移动到图层列表的顶部并隐藏POI标签图层。

1. 在图层列表中，单击**建筑物**图层并将其拖到图层列表的顶部。
2. 点击 _poi标签_ 层。
3. 单击图层列表顶部的{{<Icon name='noeye' inline={true} />}} **隐藏图层** 按钮来隐藏图层。

您可以使用 {{<Icon name='noeye' inline={true} />}} **隐藏图层**按钮来隐藏不想在最终地图样式中显示的任何图层。

### 更改建筑颜色

建筑物默认的黑色很难区分细节，因此这种样式将会使用较浅的颜色。

单击**颜色**字段并将其更改为{{<ColorSwatch color="#778899" />}}。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioChangeColor"
    alt="Screenshot showing how to adjust the layer color in Mapbox Studio"
  />
}}

### 更改摄像机间距

因为默认地图视图看起来是垂直“向下”的，所以很难看到更改这些设置的效果。因此要调整间距，使3D建筑更容易被看到:

右键单击地图视图并拖动鼠标。移动地图，直到达到所需的间距。

{{
  <Video
    filename={ChangePitch}
    title="Video showing how to change the pitch in Mapbox Studio."
  />
}}

### 调整样式的光照

更改填充拉伸层的光照强度可以突出建筑细节，使得不同的建筑易于区分。

1. 在屏幕右上角的工具栏中，单击 {{<Icon name='sun' inline={true} />}}**光照**选项卡打开 _拉伸灯光_ 面板。
2. 使用 _强度_ 滑块将光强更改为`0.75`。

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioExtrusionLighting"
    alt="Screenshot showing the extrusion lighting panel in Mapbox Studio"
  />
}}

## 发布样式

完成编辑新地图样式后，您可以发布您的更改。

1. 点击屏幕右上角的**发布**按钮。当您点击发布按钮时，将会有一个窗口显示上一版本和当前版本之间的差异。
2. If you're happy with the edits you made, click **Publish**. Your style will now be available to share from a variety of tools and applications. Click the **Share** button in the top toolbar to see all options.2.如果您对所做的编辑满意，请点击 **发布**。您的样式就可以分享到各种工具和应用程序中。单击顶部工具栏中的**共享**按钮查看所有选项。

## 完成

你已经完成了用3D建筑图层创建一个新的地图样式。

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjj0b5ie80ec32so5uo8ox21m.html?fresh=true&access_token=MapboxAccessToken#15/40.751589/-73.986485/-28/60" />
}}

## 接下来

有许多可以使用新的Mapbox工作空间样式的方法。您可以在您的网站上、在网络或移动应用程序中使用该地图。查看地图框工作室手册的 [发布样式部分](https://docs.mapbox.com/studio-manual/overview/publish-your-style/)，以了解使用地图样式的更多方法。
