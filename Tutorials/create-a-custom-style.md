---
title: Create a custom style
description: Alter a template style to create a custom map style.
thumbnail: createACustomStyle
level: 1
topics:
- map design
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { Video } from '../../components/video';"
  - "import BuildingZoom from '../../video/create-a-custom-style-building-zoom.mp4';"
contentType: tutorial
---

This guide will walk through how to create a custom style in the **Mapbox Studio style editor**. The Mapbox Studio Basic style is customizable, which lets you create a map style that conforms to your company's branding. This tutorial will show you how to customize the Mapbox Basic style by changing colors, fonts, and label properties. After you have completed the tutorial, you will have created a map style that reflects the Mapbox brand colors at any zoom level and at any place across the world.

{{
  <DemoIframe src="https://api.mapbox.com/styles/v1/examples/cji3d7gpt1i8m2rn7l7w0vl99.html?access_token=MapboxAccessToken#9.7/37.758664/-122.233084/0" />
}}

## Getting started

You will need a few resources to get started:

- **Mapbox account**. Sign up for a free account on [Mapbox](https://account.mapbox.com/auth/signup/).
- **Style guidelines**. It is often helpful to start a new custom map style with some broad style guidelines. Mapbox's brand has three primary colors (blue, gray, and pink) and a broader set of secondary colors. Every hue includes a dark, light, and faint variation. This tutorial will use a combination of these colors to style the background, water, buildings, and labels in a custom map style.

## Create a new style

Log in to your Mapbox account and navigate to the [Styles](https://studio.mapbox.com/styles) page. This is where all your map styles are listed. A [style](/help/glossary/style/) is a set of rules that defines how Mapbox draws your map on the page. It includes references to your data, map images (icons, markers, and patterns), fonts, and defines how all your data should be styled on the map. For more information about styles, read the [Styles](https://docs.mapbox.com/studio-manual/reference/styles/) section of the Mapbox Studio Manual.

To create a new style from your [Styles](https://studio.mapbox.com/styles) page, click the **New style** button. Find the _Basic Template_ style and click **Customize Basic Template**.

The Mapbox Studio style editor will open, and you will be able to start creating a custom map style.

## Customize your style

### The style editor

The **Mapbox Studio style editor** is a visual tool for creating custom map styles. Look at the layers on the left side of the style editor screen. Each layer can be customized in a variety of ways, including by changing its colors. You can also filter layers within the layer list and edit the properties of multiple layers at once. This is the easiest way to change the color of layers with similar properties. To learn more about the Mapbox Studio style editor, visit the [Mapbox Studio Manual](https://docs.mapbox.com/studio-manual/reference/styles/).

In this section, you will change the color of the water, background, and building layers and alter the fonts for various labels to create a customized map.

But first, change the name of your new style. Click into the name field in the upper left side of the screen and change the name to _Mapbox Style_.

### Style background and water layers

When the style editor first opens with the Basic style template, the map is zoomed in at a high level. Zoom out to approximately zoom level 10 so that you can see a larger geographic region. In the search bar, type in San Francisco (or another region that gives you a good mix of water, land, and city features).

{{
  <AppropriateImage
    imageId="createACustomStyleSearchBar"
    alt="Mapbox Studio screenshot showing the map's search bar"
  />
}}

You will start by altering the water and background layers so they match the colors from the Mapbox style guide.

#### Style the water layer

You will style the **water** layer with a bright blue color from the Mapbox style guide.

1. Click on the **water** layer in the layer list. When the layer panel opens, click on the **Color** field if it is not highlighted already.
2. Change the color to {{<ColorSwatch color="#314CCD" />}}.

{{
  <AppropriateImage
    imageId="createACustomStyleBackgroundWater"
    alt="Mapbox Studio screenshot showing the water layer panel"
  />
}}


#### Style the background layer by zoom level

Mapbox Studio lets you adjust styles based on specific data. In this case, you will use the style editor to change the color of the style's background based on the zoom level. Using zoom properties, the background color will become gradually lighter as the map zooms in. To style the background layer by zoom level:

1. Click on the **background** layer in the layer list.
2. When the layer panel opens, click the **Color** option if it's not already highlighted.
3. Click on **Style across zoom range**.
4. In the _Zoom_ panel, edit the first stop so the zoom level is `6` and the color is {{<ColorSwatch color="#A9B6EF" />}}. Click **Done**.
5. Click on the second stop to open its _Zoom_ panel. Change the zoom level to `12` and the color to {{<ColorSwatch color="#EDF0FD" />}}. Click **Done**.

{{
  <AppropriateImage
    imageId="createACustomStyleBackgroundColor"
    alt="Mapbox studio screenshot showing how to add a color for a specific zoom level"
  />
}}

Now, when you zoom in, the background color changes gradually as the zoom level increases.

### Style the landuse and national park layers

Now that you have changed the colors for the water and background layers, the green color that is used in the Basic style looks too bold. You will change the color of these layers to a light green from the style guide's secondary colors.

1. Select the **national_park** layer.
2. When the layer panel opens, select the **Color** field. Change the **Color** field to {{<ColorSwatch color="#E8F5EE" />}}.

{{
  <AppropriateImage
    imageId="createACustomStyleLayerNoDataCondition"
    alt="Mapbox Studio screenshot showing how to change the color for a layer without data conditions"
  />
}}

3. Select the **landuse** layer.
4. Click on the **Color** field if it is not highlighted already.
5. Click the "`class` is **park, pitch**" condition.
6. Change the **Color** field to {{<ColorSwatch color="#E8F5EE" />}}.

{{
  <AppropriateImage
    imageId="createACustomStyleLayerWithDataCondition"
    alt="Mapbox Studio screenshot showing how to change the color for a layer with data conditions"
  />
}}

### Update fonts

Next, alter the fonts that are used as labels in your style.

1. Click {{<Icon name='filter' inline={true} />}} **Filter layers** at the top of the layers list.
2. Choose **Filter by value**.
3. Choose **Fonts**.
4. Select `Roboto Black`. This will return the only layer in which this font is being used, **state-label**.
5. Click on **state-label**, then click on **Font**. Change the font to `Roboto Condensed Bold`.
6. Click on {{<Icon name='filter' inline={true} />}} **Filter layers** again, and repeat this process for the font `Roboto Regular`, which you will change to `Roboto Medium`.
    - *You can select multiple layers at once by holding down* `command` *(Mac) or* `CTRL` *(Windows) while clicking to select layers*

{{
  <AppropriateImage
    imageId="createACustomStyleFontsProp"
    alt="Mapbox Studio screenshot showing how to change font options"
  />
}}

### Style labels

After you have changed the fonts and set some general options, it's time to update the colors of the various label types used in your style.

<!--copyeditor disable clear-->

1. Click {{<Icon name='filter' inline={true} />}} **Filter layers** at the top of the layers list and search for the word _label_. This search will return 9 layers with the word _label_ in their names.
2. Select **country-label**.
3. When the layer panel opens, select the **Color** field and change it to {{<ColorSwatch color="#ffffff" />}}.
4. Change the **Halo color** field to {{<ColorSwatch color="#314CCD" />}}.
5. Change the following label layers to have the following attributes:
  - **place-neighborhood-suburb-label**: `color` {{<ColorSwatch color="#EE4E8B" />}}, `halo color` {{<ColorSwatch color="#ffffff" />}}
  - **place-city-label**: click **Clear value** and then specify the `color` {{<ColorSwatch color="#ffffff" />}}, `halo color` {{<ColorSwatch color="#273D56" />}}

{{
  <AppropriateImage
    imageId="createACustomStyleFontsPlace"
    alt="Mapbox Studio change style of place labels"
  />
}}

<!--copyeditor enable clear-->

### Style buildings

Next, change the color of the buildings in your style to a color from the Mapbox style guide:

1. Click on the **building** layer in the layer list.
2. When the layer panel opens, change the **Color** field to {{<ColorSwatch color="#aab7ef" />}}.
3. Change the **1px stroke** field to {{<ColorSwatch color="#aab7ef" />}}.

{{
  <AppropriateImage
    imageId="createACustomStyleBuildings"
    alt="Mapbox Studio screenshot of how to change building color"
  />
}}

To make sure that Mapbox template styles are performant, layers are not included at every zoom level. The building layer, for example, is visible only at zoom levels 15 and higher. You can use a zoom function to create a fade-in effect as you zoom past level 15 rather than buildings showing up abruptly once you hit zoom level 15:

1. In the **Opacity** field of the **building** layer, select **Style across zoom range**.
2. Click **Edit** to open and edit each stop:
    - Edit the first stop so the zoom level is `15` and the opacity is `0`. To change the opacity, move the opacity slider all the way to the left.
    - Edit the second stop so the zoom level is `16` and the opacity is `1`.
3. Zoom in to see the buildings fade between zoom level 15 and 16.

{{
  <Video
    filename={BuildingZoom}
    title="Mapbox Studio video showing building fade effect when zooming"
  />
}}

This fade-in effect could also be applied to roads, parks, waterways, and any other layers you choose.

## Publish

When you have finished editing your map style, publish your changes by clicking **Publish** in the upper right side of the screen. When you click the publish button, a window will display the difference between the previous and current version of this style. If you're happy with the changes, click **Publish**. Your style will now be available to share from a variety of tools and applications.

{{
  <AppropriateImage
    imageId="createACustomStylePublish"
    alt="Mapbox Studio screenshot showing how to publish a style"
  />
}}

## Finished product

You have created a map that reflects the Mapbox style guide, from a world view to the street level and at any location across the world. Explore your finished custom map style and take some time to view the style at various zoom levels.

{{
  <DemoIframe src="https://api.mapbox.com/styles/v1/examples/cji3d7gpt1i8m2rn7l7w0vl99.html?access_token=MapboxAccessToken#9.7/37.758664/-122.233084/0" />
}}

## Next steps

Mapbox Studio provides a wide variety of ways to use your new map style. You can use this map directly on your website or in a web or mobile application. Take a look at the [Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) of the Mapbox Studio Manual to see all the ways you can use your style!
