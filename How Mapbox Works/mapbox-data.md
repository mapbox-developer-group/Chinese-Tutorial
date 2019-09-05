---
title: Our map data
description: Learn about Mapbox’s map data, where it comes from, and how you can leverage it in your next project.
image: /img/narrative/data.svg
topics:
  - data
prependJs:
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: guide
---

All the data that appears in our template map styles comes from one of four Mapbox tilesets. A [tileset](/help/glossary/tileset) is a collection of raster or vector data broken up into a uniform grid of square tiles at 22 preset zoom levels.

Tilesets can be comprised of either raster or vector tiles. Raster tilesets contain a collection of images at various zoom levels that make up a complete map. A raster tileset source makes up the [Mapbox Satellite style](https://www.mapbox.com/maps/satellite/).

The rest of our map styles are created using vector tilesets. Vector tilesets contain geometries and metadata – like road names, place names, house numbers – in a compact, structured format. Vector tiles are rendered only when requested by a client, like a web browser or a mobile app.

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-data-works.html" />
}}

Vector tilesets contain only geographic/geometric and metadata, and do not inherently have any style properties. The map on the left is the geometries that are included in the **Mapbox Terrain tileset**. The map on the right shows the **Mapbox Outdoors style**, which combines data from the `Mapbox Terrain` and `Mapbox Streets` tilesets and applies styling rules to the data to create the map you see in your browser. See the [Map design guide](/help/how-mapbox-works/map-design/) for more information on how map styles work.

All our template map styles are built using some combination of our Mapbox tilesets:

- **Mapbox Streets** includes streets, buildings, areas, water, and land data based on [OpenStreetMap](http://www.openstreetmap.org/).
- **Mapbox Terrain** includes a worldwide elevation data set complete with contours, hillshade, and landcover data.
- **Mapbox Traffic** provides congestion information that is constantly updated every 5 minutes, with road geometries originating from OpenStreetMap.
- **Mapbox Satellite** includes a global satellite imagery from [a range of sources](https://www.mapbox.com/about/maps), processed and seamed together by Mapbox. You can read more about our satellite imagery in the [Satellite imagery guide](/help/how-mapbox-works/satellite-imagery).

You can also [create your own tilesets](/help/how-mapbox-works/uploading-data/) in Mapbox Studio and add the to your map alongside any Mapbox tilesets you're already using.

## How our data works

This guide covers Mapbox vector tilesets, which are the main source of Mapbox-provided data you'll work with if you're using Mapbox tools. For more information about our raster tilesets, see the [Satellite imagery guide](/help/how-mapbox-works/satellite-imagery).

### Vector tilesets

Working with vector tilesets opens up additional features for building dynamic maps, including:

- **Dynamic styling**. Using Mapbox GL JS or the Mapbox Maps SDKs for Android and iOS, you can adjust your map's appearance dynamically, without having to download new tiles.
- **Smooth interactions**. Because all your map data is loaded in the map client, you can re-render the map quickly, enabling smooth zooming, tilt, and rotation.
- **Size and speed**. While the vector tile format is not inherently small or performant, Mapbox's cartographers have done a lot of work to make sure that Mapbox-provided vector tiles are well balanced between level of detail and performance.
- **Dynamically querying**. You can use this feature to access your map data's properties right from your vector tileset.

Mapbox provides three different vector tilesets that you can use in your maps. Note that not all data included in a tileset exists at every zoom level. To keep maps lightweight, Mapbox cartographers have carefully chosen which data should appear at each zoom level.

Read about the [Mapbox vector tile specification](https://docs.mapbox.com/vector-tiles/specification/), and see a complete list of all layers included in each Mapbox vector tileset in the layer references: [Mapbox Streets v8](https://docs.mapbox.com/vector-tiles/reference/mapbox-streets-v8/#layer-reference), [Mapbox Terrain](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain/#layer-reference), [Mapbox Traffic v1](https://www.mapbox.com/vector-tiles/reference/mapbox-traffic-v1/#layer-reference).

### Data sources

The data in Mapbox tilesets come from a variety of sources.

#### Mapbox Streets

Mapbox Streets is a Mapbox-provided tileset that includes features like streets, buildings, and places from all around the world. The Mapbox Streets tileset is powered by open data from OpenStreetMap. Think of OpenStreetMap as the Wikipedia of maps. It’s a project founded on the belief that when data is open, everyone can work together to build the map. Anyone can quickly add roads and buildings to keep up with a changing world.

The Mapbox Streets tileset is updated regularly as features are edited or added to the map, which means that if you edit OpenStreetMap, you will eventually see your changes reflected on your Mapbox map. To learn more about how you can contribute to OpenStreetMap, read [our OpenStreetMap mapping guides](https://www.mapbox.com/mapping/).

To learn more about how Mapbox contributes to the OpenStreetMap community, read the [OpenStreetMap wiki entry on Mapbox](http://wiki.openstreetmap.org/wiki/Mapbox).

##### Quality assurance

<!--copyeditor ignore made-->

Besides the daily efforts of contributors all over the globe, the OpenStreetMap community uses several other methods for identifying errors in the data, including multiple [quality-assurance feedback tools](http://wiki.openstreetmap.org/wiki/Quality_assurance) and a [flagging system](http://wiki.openstreetmap.org/wiki/Vandalism) that allows users to identify where a mistake may have been made, or areas that may need special attention from someone with local knowledge.

Mapbox is also home to a dedicated OpenStreetMap data team, who are committed both to ensuring the quality of the map and also to adding and improving features all over the world. We also use an automated quarantine system that detects changes to the map that look like accidental editing mistakes or vandalism and stages them for manual review by our data team.

#### Mapbox Terrain

Mapbox Terrain is a Mapbox-provided tileset that includes features like topography, hillshades, and landcover. Mapbox Terrain is comprised of a wide variety of data sources from government-provided datasets as well as third-party commercial data. To learn more about the datasets in the Mapbox Terrain tileset, visit our [mapping platform page](https://www.mapbox.com/about/maps/#data-sources).

#### Mapbox Traffic

The Mapbox Traffic is a Mapbox-provided tileset for displaying real-time traffic conditions. Mapbox Traffic is continuously updated and built from anonymous sensor data. Mapbox SDKs collect anonymous data about the map and device location to continuously update and improve your maps. To learn more about the telemetry data that goes into the Mapbox Traffic tileset, visit [our telemetry page](https://www.mapbox.com/telemetry/).

### Mapbox Terrain-RGB

**Mapbox Terrain-RGB**, our global elevation layer, contains raw height values in meters in the Red, Green, and Blue channels of PNG tiles. You can use the elevation data stored within Terrain-RGB for a wide variety of applications both visual and analytical, from styling terrain slope and hillshades to generating 3D terrain for video games.

Terrain-RGB uses each color channel as a position in a base-256 numbering system, allowing for 16,777,216 unique values. We’ve mapped these to 0.1 meter height increments, which gives us the vertical precision necessary for cartographic and 3D applications.

You can use this endpoint to get Terrain-RGB tiles:

```
https://api.mapbox.com/v4/mapbox.terrain-rgb/{z}/{x}/{y}.pngraw?access_token={{ <UserAccessToken /> }}
```

Then use this equation to decode pixel values to height values:

```
height = -10000 + ((R * 256 * 256 + G * 256 + B) * 0.1)
```

See our [Access elevation data](/help/troubleshooting/access-elevation-data/) troubleshooting guide for more information.

### Mapbox map projections

Mapbox supports the popular [Web Mercator](http://docs.openlayers.org/library/spherical_mercator.html) projection, and does not support any other projections. Web Mercator is a nearly conformal projection that is adopted by the vast majority of web maps and its use allows you to combine Mapbox's maps with other layers in the same projection.

Commonly this projection is referred to as `EPSG:900913` or `EPSG:3857`. See [epsg.io for more information and alternative encodings](http://epsg.io/3857).

## Using our data

You can use our map data as source data for your map styles in Mapbox Studio, access our data directly using the Mapbox Maps Service APIs, or contribute to our data sources through OpenStreetMap.

### Mapbox Studio

You can use our tilesets directly in Mapbox Studio on the [Tilesets page](https://www.mapbox.com/studio/tilesets). Any time you create a new style from a template style in the Mapbox Studio style editor, you will be using a Mapbox tileset.

### Mapbox Maps Service APIs

With the [Mapbox Maps Service APIs](https://docs.mapbox.com/api/maps/), you can request Mapbox tilesets programmatically:

- [Retrieve vector tiles](https://docs.mapbox.com/api/maps/#vector-tiles) with the **Vector Tiles API**
- [Retrieve features from vector tiles](https://docs.mapbox.com/api/maps/#retrieve-features-from-vector-tiles) with the **Tilequery API**
- [Retrieve TileJSON metadata](https://docs.mapbox.com/api/maps/#retrieve-tilejson-metadata) with the **Tilesets API**

### Contribute to OpenStreetMap

We contribute to OpenStreetMap, and you should too!

[Sign up for a free account](https://www.openstreetmap.org/user/new) to start contributing. The OpenStreetMap web editor allows you to draw or edit features such as roads, buildings, parks, traffic signals, and labels. Read [Learn OpenStreetMap](http://learnosm.org/en/) for a step-by-step guide to start contributing to the project.

We've covered how Mapbox works with OpenStreetMap data, the quality controls behind it, and how you can be a part of this growing movement to provide a free and open data set for everyone.
