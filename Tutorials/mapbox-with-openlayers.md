---
title: Use Mapbox with OpenLayers
description: Learn how to use Mapbox with OpenLayers.
thumbnail: openLayersThumb
level: 2
topics:
- third party integration
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import * as constants from '../../constants';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

You can use [Mapbox](https://www.mapbox.com/developers/api/) styles with
[OpenLayers](http://openlayers.org/two/). Choose the version of OpenLayers and Mapbox tool that you're working with to get started.

{{
  <DemoIframe gl={false} src="/help/demos/openlayers/openlayers3.html" />
}}

## Getting started

There are a few things you'll need to gather before you can start working with your Mapbox maps in OpenLayers:

- **Your Mapbox access token**. You can find your access tokens on your Mapbox [Account page](https://www.mapbox.com/account/).
- **A style URL**. You can find a [style URL](/help/glossary/style-url/) in your Mapbox account's [styles](https://www.mapbox.com/studio/styles/) page.

## OpenLayers 3.x

You can load a [Mapbox Studio style or Mapbox style URL](#mapbox-studio-style-or-mapbox-style-url) or a [Mapbox tileset ID](#mapbox-tileset-id) with [OpenLayers 3.x](http://openlayers.org/).

{{
  <DemoIframe gl={false} src="/help/demos/openlayers/openlayers3.html" />
}}

### Mapbox Studio style or Mapbox style URL

To use a [Mapbox Studio style](https://www.mapbox.com/studio/styles/) or a [Mapbox style URL](/help/glossary/style-url/) with OpenLayers 3.x, you'll need to reference the [Mapbox Static Tiles API](https://docs.mapbox.com/api/maps/#static-tiles). You can replace the style URL `mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}` with your own.

```js
var map = new ol.Map({
  layers: [
    new ol.layer.Tile({
      source: new ol.source.XYZ({
        url: 'https://api.mapbox.com/styles/v1/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}/tiles/256/{z}/{x}/{y}?access_token={{ <UserAccessToken /> }}'
      })
    })
  ],
  target: 'map',
  view: new ol.View({
    center: [0, 0],
    zoom: 2
  })
});
```

### Mapbox tileset ID

To use a [Mapbox tileset ID](/help/glossary/tileset-id/) with OpenLayers 3.x, you'll need to reference the [Mapbox Raster Tiles API](https://docs.mapbox.com/api/maps/#raster-tiles). You can replace the tileset ID `mapbox.satellite` with your own.

```js
var map = new ol.Map({
  layers: [
    new ol.layer.Tile({
      source: new ol.source.XYZ({
        url: 'https://api.mapbox.com/v4/mapbox.satellite/{z}/{x}/{y}.png?access_token={{ <UserAccessToken /> }}'
      })
    })
  ],
  target: 'map',
  view: new ol.View({
    center: [0, 0],
    zoom: 2
  })
});
```

## OpenLayers 2.x

For OpenLayers 2.x, use the [OpenLayers.Layer.XYZ](http://dev.openlayers.org/docs/files/OpenLayers/Layer/XYZ-js.html) class. You can load a [Mapbox Studio style or Mapbox style URL](#mapbox-studio-style-or-mapbox-style-url-1) or a [Mapbox tileset ID](#mapbox-tileset-id-1) with OpenLayers 2.x.

{{
  <DemoIframe gl={false} src="/help/demos/openlayers/openlayers2.html" />
}}

### Mapbox Studio style or Mapbox style URL

To use a [Mapbox Studio style](https://www.mapbox.com/studio/styles/) or a [Mapbox style URL](/help/glossary/style-url/) with OpenLayers 2.x, you'll need to reference the [Mapbox Static Tiles API](https://docs.mapbox.com/api/maps/#static-tiles). You can replace the style URL `mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}` with your own.

```js
var myLayer = new OpenLayers.Layer.XYZ(
  'My Map Layer',
  ['https://api.mapbox.com/styles/v1/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}/tiles/256/${z}/${x}/${y}?access_token={{ <UserAccessToken /> }}'],
  {
    sphericalMercator: true,
    wrapDateLine: true
  }
);
var map = new OpenLayers.Map({
  div: 'map',
  layers: [myLayer],
  center: [0, 0],
  zoom: 1
});
```

### Mapbox tileset ID

To use a [Mapbox tileset ID](/help/glossary/tileset-id/) with OpenLayers 2.x, you'll need to reference the [Mapbox Raster Tiles API](https://docs.mapbox.com/api/maps/#raster-tiles). You can replace the `mapbox.satellite` with your own.


```js
var myLayer = new OpenLayers.Layer.XYZ(
  'My Map Layer',
  ['https://a.tiles.mapbox.com/v4/mapbox.satellite/${z}/${x}/${y}.png?access_token={{ <UserAccessToken /> }}'],
  {
    sphericalMercator: true,
    tileSize: new OpenLayers.Size([512, 512]),
    wrapDateLine: true
  }
);
var map = new OpenLayers.Map({
  div: 'map',
  layers: [myLayer],
  center: [0, 0],
  zoom: 1
});
```
