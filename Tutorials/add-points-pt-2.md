---
title: "Add points to a web map, part 2: create a style"
description: Add a tileset to a template style and upload custom icons in Mapbox Studio.
thumbnail: addPointsPt2
level: 1
topics:
- uploads
- map design
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
  - "import { Video } from '../../components/video';"
  - "import Publish from '../../video/add-points-pt-2-publish.mp4';"
contentType: tutorial
---

This is the second in a [series of tutorials](https://docs.mapbox.com/studio-manual/help/#add-points-to-a-map) that will teach you how to add points to a map using the Mapbox Studio dataset editor, the Mapbox Studio style editor, and Mapbox GL JS.

*Part 2* focuses on the Mapbox Studio style editor. In this tutorial, you will learn how to:

- Create a new style using one of the Mapbox default styles
- Add a tileset as a layer
- Style the new layer
- Publish your style

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjgiiz9ck002j2ss5zur1vjji.html?access_token=MapboxAccessToken#10.7/41.893748/-87.661557/0" />
}}

## Getting started

There are a few resources you will need to follow along with this guide:

- **Tileset.** You will need a tileset containing 10 Chicago parks. You can learn how to create this tileset in [Add points to a web map, Part 1: create a dataset](/help/tutorials/add-points-pt-1).
- **Custom icon.** This tutorial uses a custom icon to show the location of the parks. You will need to download the SVG icon to use in your style.

{{
<Button href="/help/data/marker-editor.svg" passthroughProps={{ download: "marker-editor" }} >
    <Icon name='arrow-down' inline={true} /> Download SVG icon
</Button>
}}

## Add data to a style

Web maps are comprised of [map tiles](/help/how-mapbox-works/web-apps/). To add your data to a web map, Mapbox will cut it up into tiles so the data can display at various zoom levels. The collection of tiles that Mapbox cuts your map into is called a tileset. In [Add points to a web map, part 1: create a dataset](/help/tutorials/add-points-pt-1), you converted a dataset into a tileset to add it to a new map style.

### Create a new style

After finishing [Add points to a web map, part 1: create a dataset](/help/tutorials/add-points-pt-1), create a new style using the Basic template. On your [Styles page](https://studio.mapbox.com/styles) in Mapbox Studio, click the **New style** button. Find the _Basic Template_ style and click **Customize Basic Template**.

The style editor will open automatically. Rename your new style to _Chicago Parks_ using the title field in the upper left side of the screen.

{{
  <AppropriateImage
    imageId="addPointsPt2RenameStyle"
    alt="Mapbox Studio style editor showing how to rename a style"
  />
}}

### Create a new layer

You will add your tileset as a new layer here:

1. When the style editor opens, click **+ Add layer** in the upper left.
2. In the list of _Data sources_, find your **chicago-parks** tileset, click the name of the tileset, and then click the source layer that appears to add it as the source for the layer.

{{
  <AppropriateImage
    imageId="addPointsPt2AddLayer"
    alt="screenshot illustrating how to add a new layer in Mapbox Studio"
  />
}}

3. Mapbox Studio recognizes that the data you have uploaded is focused on a different location, so it displays the message _"This tileset isn't available from your map view."_ Click **Go to data**, and the map view will refocus on Chicago.
4. Click the **Type** option, and then choose the _Symbol_ layer option so you can create a layer with [markers](/help/glossary/marker/).
5. Click back to the **Style** tab.

{{
  <AppropriateImage
    imageId="addPointsPt2CreateLayer"
    alt="screenshot illustrating how to create a new layer in Mapbox Studio"
  />
}}

## Style a layer

In the Mapbox Studio style editor, you can specify the style properties of each layer. This includes the layers in the Mapbox default styles and any layers you’ve added with custom data. For this example, you will style a *symbol* layer. You can style symbol layers with both text and icons.

### Style as a symbol layer

1. Click on the **chicago-parks** layer you created in the layer list on the left side of the style editor.
2. When the style panel opens, click the **Style** tab if you're not already there.
3. Select the **Icon** tab and click on **Manage icons in your spritesheet**.
4. This opens the **Images** option in the top toolbar.

{{
  <AppropriateImage
    imageId="addPointsPt2UploadSvg"
    alt="screenshot demonstrating the upload SVG menu in Mapbox studio"
  />
}}

5. Click the **Upload SVG Image** button to and choose the marker you downloaded at the beginning of this tutorial from your files.
6. Once the icon has loaded, choose it from the list.

{{
  <AppropriateImage
    imageId="addPointsPt2SelectIcon"
    alt="screenshot demonstrating the upload SVG menu in Mapbox studio"
  />
}}

7. If you would like to show all the markers, even if they overlap, click on the **Placement** tab. Scroll down to **Allow icon overlap** and set it to `True`.

You should now see the marker icon appear on all your points.

{{
  <AppropriateImage
    imageId="addPointsPt2IconsLoaded"
    alt="screenshot showing a style with a custom icon loaded in Mapbox Studio"
  />
}}

## Publish a style

Now that you have finished styling your map, you need to publish your style for those changes to be live on the web.

1. Click the **Publish** button in the top right of the editor.
2. A window will pop up asking you to review your changes.
3. Click **Publish**.

{{
  <Video
    filename={Publish}
    title="Comparing styles in the Publish modal"
  />
}}

## Share

The [Share modal](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) contains the resources you need to publish your style in a web app, mobile app, or with another third-party tool.

### Share

Click **Share** in the upper right of the style editor. The Share modal contains a share URL that allows you to share a preview of your style with others. The modal also contains a style URL and your access token, both of which you will need in [part three of this tutorial](/help/tutorials/add-points-pt-3/).

{{
  <AppropriateImage
    imageId="addPointsPt2ShareStyle"
    alt="Screenshot showing the share section for a style in Mapbox Studio"
  />
}}

## Next Steps

Head to [Add points to a web map, part 3: add interactivity](/help/tutorials/add-points-pt-3/) to add popups with information about each park to your map using Mapbox GL JS.
