---
title: Add 3D buildings to a Mapbox Studio style
description: Add a 3D building layer to a map style in Mapbox Studio.
thumbnail: add3dBuildingsStudio
topics:
- map design
level: 1
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { Video } from '../../components/video';"
  - "import ChangePitch from '../../video/add-3d-buildings-studio-change-pitch.mp4';"
contentType: tutorial
---

This tutorial will walk you through the process of adding a 3D building layer to a map style using Mapbox Studio.

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjj0b5ie80ec32so5uo8ox21m.html?fresh=true&access_token=MapboxAccessToken#15/40.751589/-73.986485/-28/60" />
}}

## Getting started

Before you start this tutorial, you need to create a **Mapbox account** by signing up at [mapbox.com/account](https://account.mapbox.com).

## Create a new style

To begin, you will create a new map style in Mapbox Studio.

1. Log in to your Mapbox account and navigate to the [Styles](https://studio.mapbox.com/styles) page.
2. Click the **New style** button. Find the _Basic Template_ style and click **Customize Basic Template**.
3. In Mapbox Studio style editor, rename this new style so that you can find it later. Click into the title field in the upper left side of the screen and change the title to _3D buildings_.
4. In the search bar in the upper right corner, type in "Empire State Building" and select the first result.

{{
<AppropriateImage 
  imageId="add3dBuildingsStudioLocationSearch"
  alt="Screenshot showing a new map view in Mapbox Studio"
/>
}}

The map view will move so that it is centered on the Empire State building in New York City.

## Edit the building layer

Next, you will edit the style's building layer.
<!--copyeditor ignore okay-->
1. In the layer panel on the left side of the screen, select the **building** layer.
2. Click **Select data**. This opens the x-ray view, which displays the data from the building layer.
3. Click the **Type** option in the _New layer_ panel and select the _Fill extrusion_ option. If prompted to do so, click **Okay** to confirm that you want to change the layer's type.
4. Remove all existing filters on this layer.
5. Click **+ Create filter** and select the **extrude** data property.
6. Leave the dropdown menu set to _is any of_ and click the **Empty** button.
7. Select **true**.
8. Click the **Style** option to return to the building layer's styling panel.

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioEditFilter"
    alt="Screenshot showing how to edit a layer filter in Mapbox Studio"
  />
}}

Now that the building layer's type has been changed, its style settings need to be adjusted to show the desired 3D effect.

{{ <Note imageComponent={<BookImage />}> }}
This tutorial takes advantage of the building layer in Mapbox Streets v7. If you have custom building data that you would like to use in a map style instead, that data can be uploaded to Mapbox as a tileset using either [Mapbox Studio](https://studio.mapbox.com/tilesets/) or the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads).
{{ </Note> }}

## Adjust the layer's style settings

Next, you will adjust the layer's height and base height properties to achieve the desired 3D effect.

### Set the height property

1. Select the _building_ layer and click on the **Height** property.
2. Choose the **Style across data range** option.
3. In the _Choose a numeric data field_ panel, click on **height**.

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioStyleHeight"
    alt="Screenshot showing the style across data range option in Mapbox Studio"
  />
}}

4. The first stop is already set to a _height_ of `0` and a _Fill height_ of `0`. Leave these settings as they are.
5. In the second stop, leave the _height_ set to `999` and change the _Fill height_ option to `999`.

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioStyleMaxHeight"
    alt="Screenshot showing the style max height option in Mapbox Studio"
  />
}}

### Set the base height property

The base height property of the layer also needs to be adjusted. This will handle any cases where a building has a base as well as a separate taller part that has a different architectural shape. If you do not set the base height property, then buildings will lose some of their nuanced architectural features.

1. Select the _building_ layer and click on **Base height**.
2. Choose the **Style across data range** option.
3. In the _Choose a numeric data field_ panel, select **min_height**.
4. The first stop is already set to a _height_ of `0` and a _Fill base height_ of `0`. Leave these settings as they are.
5. In the second stop, leave the _height_ set to `999` and change the _Fill base height_ option to `999`.

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioFillBaseHeight"
    alt="Screenshot showing how to adjust the base height setting in Mapbox Studio"
  />
}}

### Make the layer more prominent

Since the building layer has many items above it in the layers list, those items render on top of the buildings in this style. To make the buildings more prominent, you will move the building layer to the top of the layers list and hide the POI label layer.

1. In the layers list, click and drag the **building** layer to the top of the layer list.
2. Click on the _poi-label_ layer to select it.
3. Click on the {{<Icon name='noeye' inline={true} />}} **Hide layer** button at the top of the layer list to hide the layer.

You can use the {{<Icon name='noeye' inline={true} />}} **Hide layer** button to hide any layer that you do not want to display in your final map style.

### Change the building color

The default black color of the buildings makes it hard to distinguish details, so this style will use a lighter color.

Click on the **Color** field and change it to {{<ColorSwatch color="#778899" />}}.

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioChangeColor"
    alt="Screenshot showing how to adjust the layer color in Mapbox Studio"
  />
}}

### Change the camera pitch

It's difficult to see the impact of changing these settings because the default map view looks straight "down". To adjust the pitch and make the 3D buildings easier to see:

Right click on the map view and drag the mouse. Move the map until you reach the desired pitch.

{{
  <Video
    filename={ChangePitch}
    title="Video showing how to change the pitch in Mapbox Studio."
  />
}}

### Adjust the style's lighting

Changing the lighting intensity for a fill extrusion layer highlights architectural details and makes it easier to distinguish between different buildings.

1. In the toolbar on the upper right side of the screen, click the {{<Icon name='sun' inline={true} />}} **Light** tab to open the _Extrusion Lighting_ panel.
2. Use the _Intensity_ slider to change the light intensity to `0.75`.

{{
  <AppropriateImage
    imageId="add3dBuildingsStudioExtrusionLighting"
    alt="Screenshot showing the extrusion lighting panel in Mapbox Studio"
  />
}}

## Publish the style

When you have finished editing your new map style, you will publish your changes.

1. Click the **Publish** button in the upper right side of the screen. When you click the publish button, a window will display the difference between the previous version and the current version.
2. If you're happy with the edits you made, click **Publish**. Your style will now be available to share from a variety of tools and applications. Click the **Share** button in the top toolbar to see all options.

## Finished product

You have created a new map style with a 3D building layer.

{{
<DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjj0b5ie80ec32so5uo8ox21m.html?fresh=true&access_token=MapboxAccessToken#15/40.751589/-73.986485/-28/60" />
}}

## Next steps

There are many different ways that you can use your new Mapbox Studio style. You can use this map on your website, or in a web or mobile application. Take a look at the [Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) of the Mapbox Studio Manual to read about all the ways you can use your map style.
