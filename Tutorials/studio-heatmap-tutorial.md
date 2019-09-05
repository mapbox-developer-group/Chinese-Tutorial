---
title: Make a heatmap with Mapbox Studio
description: Learn how to add and configure a heatmap layer using Mapbox Studio.
thumbnail: studioHeatmapTutorial
topics:
- web apps
- map design
level: 1
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

A heatmap is a way of representing data that allows you to visualize both data point density as well as the relative differences between points based on data properties. They are a visually engaging way to encourage your audience to explore the data displayed on your map.

In this tutorial, you will use Mapbox Studio to create a heatmap that displays the location of meteorite strikes around the world, based on data collected by NASA. You will also use the weight of each meteorite in grams to display the relative size of each meteorite.


{{
  <DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjikt35x83t1z2rnxpdmjs7y7.html?access_token=MapboxAccessToken#2/11.285/-65.322/0" />
}}

## Getting started

To complete this tutorial, you will need:

- **A Mapbox account and access token.** Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your access tokens on your [Account page](https://account.mapbox.com).
- **Meteorite strike data.** In this tutorial, you will be using information about meteorite strikes from [NASA's open data portal](https://data.nasa.gov/Space-Science/Meteorite-Landings/gh4g-9sfh). Download this CSV file to your computer so that you can access it in the first step of the tutorial.

{{
<Button href="/help/demos/studio-heatmap/meteorites.csv" passthroughProps={{ download: "meteorites" }} >
    <Icon name='arrow-down' inline={true} /> Download CSV
</Button>
}}

## Upload your data

To add the meteorite strike information to a style in Mapbox Studio, you need to upload it to your account first. To upload this file to Mapbox Studio:

1. Go to your [**Tilesets** page](https://studio.mapbox.com/tilesets).
2. Click the **New tileset** button.
3. Import `meteorites.csv`. To do so, you can either:
  - Click **Select a file** and select the file.
  - Drag the file into the uploader.
4. Click **Confirm** to upload the file to your account.

When the upload is complete, there will be a notification icon in the lower right corner of the screen.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialUploadSuccessful"
    alt="Screenshot showing a successful file upload in Mapbox Studio"
  />
}}

## Create a new style

Now that you have uploaded the meteorite strike information as a tileset, you can add it to a new map style.

1. Go to your [Styles page](https://studio.mapbox.com/styles/) in Mapbox Studio.
2. Click the **New style** button. Find the _Basic Template_ style and click **Customize Basic Template**.
3. Now in the Mapbox Studio style editor, you will create your map style. Rename your new style so that you can find it later! Click into the title field in the upper left side of the screen and change the title to _Meteorites_.

## Add a heatmap layer

To add and style the meteorite strike data as a heatmap layer, you will need to add a new layer to the style you created.

1. At the top of the layer panel, click **+ Add layer**.
2. In the list of _Data sources_, search for "meteorites" and select the meteorite strike tileset.
3. Click the **Type** option, and select the **Heatmap** option.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialLayerType"
    alt="Screenshot showing how to change a new layer type to heatmap in Mapbox Studio"
  />
}}

4. Click the **Style** tab at the top of the panel.
5. The meteorite strike tileset is now a heatmap layer in your style. Click on the layer name and change it to "meteorite strikes".

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialLayerName"
    alt="Screenshot showing how to change a layer name in Mapbox Studio"
  />
}}

## Configure layer properties
<!-- copyeditor ignore represents -->
A heatmap layer in Mapbox Studio has several different layer property options. Understanding what these properties mean is key to creating a heatmap that accurately represents your data and strikes the right balance between showing too much detail and being a large colorful blob!

- **Color**: Defines the heatmap’s color gradient, from a minimum value to a maximum value. You can adjust the density and color of each stop individually, as well as add and delete stops.
- **Opacity**: Controls the global opacity of the heatmap layer.
- **Radius**: Sets the radius for each point in pixels. As the radius number increases, the heatmap will get smoother and less detailed.
- **Weight**: Measures how much each individual point contributes to the appearance of your heatmap. Heatmap layers have a weight of one by default, which means that all points are weighted equally. Increasing the weight property to five has the same effect as placing five points in the same location. You can use the _Style across data range_ and _Style with data conditions_ options to set the weight of your points based on specified properties.
- **Intensity**: A multiplier on top of the weight property. Intensity is primarily used as a convenient way to adjust the appearance of the heatmap based on zoom level.

### Radius

In a heatmap, the radius of the points should increase as the zoom level increases to preserve the smoothness of the heatmap as the points become more spread out. For this tutorial, you will change the default (a radius of `30 px` at all zoom levels) so that the radius increases as the map is zoomed in.

1. Select the **Radius** tab in the heatmap layer.
2. Choose **Style across zoom range**.
3. For the first stop, change the radius at zoom level `0` (zoomed out to the maximum extent) to `5 px`.
4. Click **Done**.
5. The next stop is already set at zoom level `22` (zoomed in to the maximum extent) with a radius of `30 px`. Leave this stop with these settings.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialRadius"
    alt="Screenshot showing how to adjust heatmap data point radius in Mapbox Studio"
  />
}}

### Weight

In the tileset you uploaded, the `mass(g)` property ranges from 1-60000000 grams. That's a wide range of meteorite sizes! Give more weight in your heatmap to the larger meteorites by setting stops that increase the weight of a point as the mass increases.

1. Select the **Weight** tab.
2. Click on **Style across data range**.
3. You will be prompted to choose a numeric data field on which to base the property's styling. Choose `mass(g)`.<br><br>

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialDataRange"
    alt="Screenshot showing how to choose a data field in the style across data range option"
  />
}}

4. The first stop is set to a mass of `0` and a weight of `1`. Leave this stop at these settings.
5. The next stop is already set to the maximum mass in the dataset. Change the weight to `25`.
6. Click `Done`.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialWeight"
    alt="Screenshot showing how to adjust heatmap weight in Mapbox Studio"
  />
}}

### Intensity

The intensity of the heatmap layer can be increased as the map zooms in, to preserve a similar appearance throughout the zoom range.

1. Select the layer's **Intensity** tab.
2. Click on **Style across zoom range**.
3. The first stop is set to a zoom level of `0` and an intensity of `1`. Leave this as it is.
4. Change the second stop to zoom level `22` and an intensity of `10`.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialIntensity"
    alt="Screenshot showing how to adjust heatmap intensity in Mapbox Studio"
  />
}}

These images show the impact of intensity on your style's appearance. The image on the right shows intensity that uses the default of `1`, while the image on the left shows intensity that increases with zoom level.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialIntensityComparison"
    alt="Screenshot showing the difference between default and custom heatmap intensity in Mapbox Studio"
  />
}}

### Color
Heatmap layers in Mapbox Studio come with a vibrant set of preset colors with which to represent the density of the data points. For this tutorial, though, we will change the color scheme. We've taken these colors from a color recommendation site that's specifically for cartography, [Color Brewer](http://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3).

1. Select the **Color** tab in the heatmap layer.
2. The first stop has a density of `0` and an opacity of `0`. Without these settings, the meteorite layer would be opaque, obscuring the rest of the map. Leave this stop at these settings.
3. Click on the second stop, which has a density of `0.1`. Change the color to {{<ColorSwatch color="#ffffb2" />}}.
4. Click **Done**.
5. Adjust the remaining density stops with the following colors:
  - `0.3`: {{<ColorSwatch color="#feb24c" />}}
  - `0.5`: {{<ColorSwatch color="#fd8d3c" />}}
  - `0.7`: {{<ColorSwatch color="#fc4e2a" />}}
  - `1.0`: {{<ColorSwatch color="#e31a1c" />}}

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialColor"
    alt="Screenshot showing how to change heatmap stop colors in Mapbox Studio"
  />
}}

### Opacity
Your heatmap is looking good, but it's difficult to read location labels since the meteorite strike points obscure them. Adjust the heatmap layer's opacity so that you can read the labels:

1. Select the **Opacity** layer.
2. Change the opacity to `0.7`, either by using the slider bar or by typing the number in directly.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialOpacity"
    alt="Screenshot showing how to change heatmap layer opacity in Mapbox Studio"
  />
}}

## Publish

When you finish editing your map style, publish your changes by clicking **Publish** in the upper right side of the screen. When you click the publish button, a window will display the difference between the previous and current version of this style. If you're happy with the changes, click **Publish**. Your style will now be available to share from a variety of tools and applications.

{{
  <AppropriateImage
    imageId="studioHeatmapTutorialPublish"
    alt="Screenshot showing how to change heatmap stop colors in Mapbox Studio"
  />
}}

If you go back to your Styles page, you will see your new style at the top of the list.

## Finished product

You have created a style that displays meteorite strike data from around the world, in a way that also allows you to show the relative mass of each meteorite.

{{
  <DemoIframe src="https://api.mapbox.com/styles/v1/examples/cjikt35x83t1z2rnxpdmjs7y7.html?access_token=MapboxAccessToken#2/11.285/-65.322/0" />
}}


## Next steps

Mapbox Studio gives you a variety of ways to use the new map style you created. You can use this map directly on a website or in a web or mobile application. Take a look at the [Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) of the Mapbox Studio Manual to learn about the different ways you can use your style.
