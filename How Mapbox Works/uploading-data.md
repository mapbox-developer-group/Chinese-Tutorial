---
title: Upload data
description: Learn the difference between tilesets and datasets, how the upload process works, and techniques for uploading.
image: /img/narrative/data-upload.svg
topics:
  - uploads
contentType: guide
---

Mapbox allows you to upload your own custom data to be converted into a **tileset** or **dataset**. This guide outlines the differences between tilesets and datasets, how the upload process works, techniques for uploading, and resources for getting started.

<!-- <div style='width:100%;height:300px;background-color:#eee' class='mb24'></div> -->

## How uploads work

Mapbox stores your data in formats that are optimized for display in interactive web maps. Depending on the type of data you upload and the desired use case, your data will either be stored as raw [GeoJSON](/help/glossary/geojson/) or will be processed into a raster or vector [tileset](/help/glossary/tileset/).

There are two possible avenues for uploading data to your Mapbox account, each of which comes with its own set of considerations:

- The [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) is designed to accept many common geospatial file types, which, when uploaded, are automatically processed into [vector tiles](/help/glossary/vector-tiles/). Tilesets can be uploaded via the Tilesets page in Mapbox Studio or programmatically using the Mapbox Uploads API. A tileset can be created from uploaded data, or it can be created from an existing [dataset](/help/glossary/dataset).
- The [Mapbox Datasets API](https://docs.mapbox.com/api/maps/#datasets) is designed to store raw [GeoJSON](/help/glossary/geojson/) as datasets. Datasets can be uploaded via the Datasets page in Mapbox Studio or programmatically using the Mapbox Datasets API.

The following section provides a more detailed comparison of the Mapbox Uploads API and Datasets APIs.


### Datasets vs. tilesets

[**Datasets**](/help/glossary/dataset) and [**tilesets**](/help/glossary/tileset) are two different types of files that you can create when uploading data to your Mapbox account. Datasets are editable and tilesets are styleable.

**Datasets** provide access to feature geometries (points, lines, and polygons) and properties (attributes), both of which **can be edited** in the Mapbox Studio [dataset editor](https://www.mapbox.com/studio/datasets/) or through the Mapbox [Datasets API](https://docs.mapbox.com/api/maps/#datasets).

Consider using a dataset if you are working with less complex data that needs to be updated often. It is important to note that once your dataset has been created, it will need to be published into a tileset to be added to a style in the Mapbox Studio style editor. With datasets, you can continue to make changes to your data as needed, publish each update to the connected tileset, and see those changes reflected in any styles that contain that tileset.

![animated GIF of editing dataset in the Mapbox Studio dataset editor](/help/img/studio/dataset-modify-feature.gif)

**Tilesets** are lightweight collections of vector data that are optimized for rendering and are not *editable* but can be *styled* in the Mapbox Studio style editor. Consider uploading your data as a tileset if your data is large and doesn't need to be updated often.

![animated GIF of a tileset in the Mapbox Studio style editor](/help/img/studio/tileset-upload.gif)

### How data becomes a tileset

When you upload data as a tileset or export a dataset as a tileset, Mapbox breaks it up into a uniform grid of square tiles at preset zoom levels. It must undergo many processing steps to load quickly and be lightweight. These are the same processes [Mapbox Streets](https://www.mapbox.com/vector-tiles/) data undergoes before it becomes the global Mapbox Streets tileset you may be familiar with. When data becomes a tileset, two things happen:

**1. Simplification**

The Mapbox Uploads API analyzes your data for complexity and automatically removes unnecessary vertices at variable rates depending on zoom level. This process is called *simplification*, and it helps make sure your maps load quickly, especially at lower zoom levels where additional complexity would not be visible.

**2. Determining the zoom extent**

The Mapbox Uploads API keeps your tilesets light by examining your data's extent (the geographic area covered by your data) and complexity and only creates vector tiles for zoom levels that are likely to be required &mdash; a [zoom extent](/help/glossary/zoom-extent/) is defined. For datasets with small zoom extents or complex features, this usually means low zoom levels (zoomed out) will be discarded. For large features that are not complex, this usually means higher zoom levels (zoomed in) will be discarded.

If you need your tileset to be visible at a different zoom extent, you can [adjust this manually](/help/troubleshooting/adjust-tileset-zoom-extent/), but it is important to note the following:

- Minimum zoom levels can be increased, but not decreased past the assigned minimum zoom level.
- Maximum zoom levels can be decreased and increased, since data can be [overzoomed](/help/glossary/overzoom/) and visualized to zoom 22.

### Raster and vector tilesets

Tilesets can be created with raster or vector data.

If you upload raster data (such as a GeoTIFF), the resulting raster tilesets will only contain raster data, a [pixel-based](https://en.wikipedia.org/wiki/Raster_graphics) data format that all digital photographs conform to.

If you upload vector data, this will create a vector tileset containing vector data, which consists of mathematically calculated points, lines, and polygons as x/y pairs. [Mapbox GL](/help/glossary/mapbox-gl/) takes advantage of vector tilesets by calculating and rendering vector data directly in your browser.

### What you can do with tilesets

If you created a vector tileset by uploading geospatial data that contains attributes, the resulting vector tileset will inherit the attributes contained in your raw data source. Here are a few examples of what you can do with the attributes belonging to features in a vector tileset:

- Use [Mapbox Studio](/help/tutorials/choropleth-studio-gl-pt-1/) to customize the color of a state based on its population density.
- Use the [Mapbox Maps SDK for iOS](https://www.mapbox.com/ios-sdk/examples/dds-circle-layer/) to dynamically style trees based on an `AGE` attribute.
- Use [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/example/query-similar-features/) to highlight counties share a similar name.

## Uploading data

There are several ways you can upload custom data as tilesets or datasets.

### Mapbox Studio

You can upload both tilesets and datasets to Mapbox Studio. Upload data as a tilesets using the [Tilesets page](https://www.mapbox.com/studio/tilesets/) in Mapbox Studio. Upload your own data as a dataset on the [Dataset page](https://www.mapbox.com/studio/datasets) in Mapbox Studio. You can also create a blank dataset and draw data directly in your browser using the Mapbox Studio dataset editor. For more information on how to create data from scratch in Mapbox Studio see [Create new data](/help/how-mapbox-works/creating-data/).

Learn more about accepted file types, transfer limits, and how to manage data in the [Mapbox Studio manual Uploads section](https://www.mapbox.com/studio-manual/overview/geospatial-data/).

### Mapbox Uploads API

You can use the Mapbox Uploads API directly to create both raster and vector tilesets programmatically. For more details on how to upload your custom data, see the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) documentation.

### Mapbox Datasets API

You can use the Mapbox Datasets API directly to create, edit, and manage datasets programmatically. For more details on how to create and work with datasets, see the [Mapbox Datasets API](https://docs.mapbox.com/api/maps/#datasets) documentation.
