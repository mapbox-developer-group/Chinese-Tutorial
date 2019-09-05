---
title: Build indoor floorplans with Mapbox
description: Upload a floorplan to create an indoor map.
thumbnail: indoorFloorplans
level: 3
topics:
- uploads
- map design
- third party integration
language:
- Varies
prereq: Familiarity with GIS.
contentType: tutorial
---

You can use Mapbox to put a floor plan or non-geographic data on our maps. There are a couple of routes you can take. The key is to give your data some geographic reference for it to work in a mapping application. You can do this in a couple of ways, depending on your data's format:

- If you want to overlay an image of your plan, you need to [georeference](/help/tutorials/georeferencing-imagery/) it.
- If you want to use a tool like [Mapbox.js](https://www.mapbox.com/mapbox.js/) to display your data as a tiled image, read [this guide](http://www.macwright.org/2012/08/13/images-as-maps.html) to learn about processing non-map images as maps.
- If you know the bounding coordinates of your image, you can use the `imageOverlay` constructor in Leaflet shown in [this example](https://www.mapbox.com/mapbox.js/example/v1.0.0/imageoverlay-georeferenced/).
- If you have data in a geographic vector format, such as GeoJSON, KML, or Shapefile, you can upload it to [Mapbox Studio](https://github.com/mapbox/mapbox-studio-classic) as a [tileset](/help/glossary/tileset/), add it to a [style](https://www.mapbox.com/studio-manual/reference/styles/), and embed it in your website using Mapbox GL JS.
- If you are using Mapbox GL JS, you can also create 3D floorplans like in [this example](https://www.mapbox.com/mapbox-gl-js/example/3d-extrusion-floorplan/) using `fill-extrusions`.
