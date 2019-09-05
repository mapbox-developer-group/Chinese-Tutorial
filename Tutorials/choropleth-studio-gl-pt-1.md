---
title: "Make a choropleth map, part 1: create a style"
description: Upload custom data to Mapbox Studio, add it to a template style, and use filters to style your data.
thumbnail: choroplethStudioGlPt1
level: 1
topics:
- uploads
- map design
- web apps
language:
- No code
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import { PRODUCTION_TOKEN, VERSION_MAPBOXGLJS } from '../../constants'"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

One way to show data distribution on a map is with a [**choropleth**](https://en.wikipedia.org/wiki/Choropleth_map), a thematic map in which areas are shaded based on a particular value. In this guide, you will use Mapbox Studio and Mapbox GL JS to make a map of US states showing population density. (If you are familiar with [Leaflet](/help/glossary/leaflet), this map [may look familiar](http://leafletjs.com/examples/choropleth/)!)

{{
  <DemoIframe src="/help/demos/choropleth-studio-gl/demo-five.html" />
}}

## Getting started

You will be using two Mapbox tools throughout this guide:

- [Mapbox Studio](/help/glossary/mapbox-studio) to add your data and create your map style.
- [Mapbox GL JS](/help/glossary/mapbox-gl-js) to add interactivity to your map and publish it on the web.

## Download the data

For this guide, you will need to download some [**data**](/help/demos/choropleth-studio-gl/stateData.geojson). This GeoJSON file is borrowed from [the Leaflet choropleth tutorial](http://leafletjs.com/examples/choropleth/) and contains data on population density across US states.

## Upload your data

To add the population density data to a style in Mapbox Studio, you need to upload it to your account. Go to your [**Tilesets** page](https://studio.mapbox.com/tilesets) in Mapbox Studio to upload your data.

On your Tilesets page, click the **New tileset** button. Select the file `stateData.geojson` and upload it to your account.

When the upload is complete, click on the arrow next to the filename to open its information page.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1DataUploadSuccess"
    alt="upload dialog leading to your tileset's information page"
  />
}}

## Inspect the tileset

When you upload vector data to your Mapbox account, our servers convert it to a [vector tileset](/help/glossary/tileset) so it can be rendered quickly and efficiently in the Mapbox Studio style editor and with Mapbox GL JS. The tileset information page shows some useful information about the tileset that was created from your uploaded data.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1StatedataPage"
    alt="new state data tileset information page"
  />
}}

- In the center, you can see the properties from the original GeoJSON file: **density** and **name**. The uploaded tileset maintains the properties from the original data file, which you can use when adding style rules for the tileset.
- The **tileset ID** is the unique identifier for this tileset.
- **Format**, **Type**, **Size**, and **Bounds** provide general information about the tileset.
- **Zoom extent** tells you the zoom levels at which tiles were generated for your uploaded data. Don't worry about this number. Vector tiles are comprised of vector data and can be [overzoomed](/help/glossary/overzoom/) and styled up to zoom level 22.

## Create a new style

After you've inspected your data, it's time to create a new style so you can put it on the map! Go to your [Styles page](https://studio.mapbox.com). Click the **New style** button. Find the _Basic Template_ style and click **Customize Basic Template**.

Excellent! Welcome to the Mapbox Studio style editor. This is where you will create your map style.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1NoData"
    alt="Mapbox Studio style editor showing default Basic style"
  />
}}

Rename the style so that you can find it later. Click into the title field in the upper left side of the screen to change the title from Basic Template to Population.

_If this is your first time in the style editor, read the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/reference/styles/) for more information on getting started._

## Add a new layer

To add and style the population density data, you will need to add a new layer to the map. At the top of the layer panel, click **+ Add layer**.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1NewLayer"
    alt="Mapbox Studio add new layer"
  />
}}

The editor is now showing your map in x-ray mode. X-ray mode shows all the data in the sources added to the style, regardless of whether there is a layer to style it.

In the _New layer_ panel, look in the list of _Data sources_ for the `statedata` source. Click the tileset and then select the source layer as the source for this new style layer.

The default Basic map view is not centered on the United States. Mapbox Studio recognizes that the data you have uploaded is focused on a different location, so it displays the message _"This tileset isn't available from your map view."_ Click **Go to data**, and the map view will refocus on the United States.

Your new layer will be highlighted on the x-ray map.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1StateDataXray"
    alt="Mapbox Studio set data dialog showing x-ray mode"
  />
}}

Click the **Style** tab and the map will switch back to style mode displaying your new layer. You will see the state data on the map with a default style (black with 100% opacity).

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1StateDataBlack"
    alt="Mapbox Studio state data with default fill-color style"
  />
}}

You can rename a layer by clicking on the name of the layer at the top of the panel. Rename your new layer `statedata`.

## Style the layer

On the original Leaflet map, the data is styled based on the population density of each state:

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1LeafletChoropleth"
    alt="original Leaflet choropleth map"
  />
}}

### Data-driven styling

In the Mapbox Studio style editor, you can assign a color to each state based on its population density. Click the **Style** link in the `statedata` layer. Next, click **Style across data range**.

Under *Choose a numeric data field*, select `density` since you want to style each state according to its population density.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1InterpolateFromData"
    alt="Mapbox Studio style editor interpolate from data"
  />
}}

The rate of change is _linear_. Click **Edit** and select **Step** instead. Click **Done**. Since you have set the rate of change to step, the colors for each range of density between stops will be uniform.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1DataSetRateChange"
    alt="Mapbox Studio style editor set the rate of change to step"
  />
}}

Now it's time to start adding stops and colors! You will create several stops to break states up into groups with similar population densities. Click on **Edit** in the first density stop. The first stop is fixed at _1.264_, based on the information in the data set you uploaded. Click on it and change the color to `#FFEDA0`. Click **Done**.

Change *density* of the next stop to `10`, and change the color to `#FFEDA0` as well. Click **Done**.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1SetFirstDensityStop"
    alt="Mapbox Studio style editor set first density stop"
  />
}}

Click **+ Add another stop**. Change *density* to `20`, and change the color to `#FED976`. Click **Done**.

Create the following additional stops:

- `50`: `#FEB24C`
- `100`: `#FD8D3C`
- `200`: `#FC4E2A`
- `500`: `#E31A1C`
- `1000`: `#BD0026`

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1SetAllDensityStops"
    alt="Mapbox Studio style editor set colors for all density stops"
  />
}}

As you start adding stops, you will see the map change on the right to reflect the new stops. In this case, all states with a population density between `0-10` will be assigned the color `#FFEDA0`, all states with population density from `10-20` will be assigned the color `#FED976`, and so on.

Give your states a fancy outline style and reduce their opacity to help your readers distinguish between neighboring states. Change the *Opacity* to `0.6`. Next, change the *1px stroke* style property to `#FFF`.

## Reorder your layers

After you've created and styled your layer, your map should look something like this:

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1DataOnTop"
    alt="screenshot of the choropleth map of the United States with custom data on top of place labels"
  />
}}

Everything looks good, except for one thing - the labels are underneath the data layer! One of the coolest things about the Mapbox Studio style editor is that you can reorder any of the elements of the map. This means you can put labels on top of your data.

Hover over your `statedata` layer. Click the {{<Icon name='menu' inline={true} />}} next to the layer's name in the layer list on the far left and drag your layer below the place labels.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1MoveStatedataLayer"
    alt="Mapbox Studio style editor move statedata layer"
  />
}}

Now that labels are on top of the population density data, city labels are popping out above the more important state labels. To turn off the city labels, click on **{{<Icon name='filter' inline={true} />}} Filter layers** and type _place_. This will return all the city label layers. Select multiple layers at once by holding down `command` (Mac) or `CTRL` (Windows) while clicking on these layers. Next, click the {{<Icon name='eye' inline={true} />}} button at the top of the layers pane to turn off these layers' visibility.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1HideLayers"
    alt="hide layers in the Mapbox Studio style editor"
  />
}}

To make the boundaries between states more visible, you can move the **admin-state-province** layer above the `statedata` layer in the layer list.

{{
  <AppropriateImage
    imageId="choroplethStudioGlPt1MoveLayers"
    alt="move layers in the Mapbox Studio style editor"
  />
}}

## Publish the style

Now that you've got your map looking good, it's time to publish! Click the **Publish** button in the top right of the screen, then click **Publish** again on the next prompt.

Hooray! Your style is now published! If you go back to your Styles page, you will see your new style at the top of the list.

## Next steps

Head to [part 2](/help/tutorials/choropleth-studio-gl-pt-2/) to learn how add interactive elements to your map and publish it to the web with Mapbox GL JS.
