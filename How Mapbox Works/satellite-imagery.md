---
title: Satellite imagery
description: Learn how satellite imagery works and how to use it in your next Mapbox project.
image: /img/narrative/satellite.svg
topics:
  - satellite
contentType: guide
---

[Mapbox Satellite](/help/glossary/mapbox-satellite) is a global basemap of high resolution satellite imagery, and [Mapbox Satellite Streets](https://www.mapbox.com/maps/satellite) combines the Mapbox Satellite basemap with vector data from [Mapbox Streets](https://www.mapbox.com/maps/streets/) to bring contextual information to your map. The imagery data comes from a variety of commercial providers, as well as open data from NASA, USGS, and others. It is color-corrected and blended together into a single raster [tileset](/help/glossary/tileset/). This guide provides an overview of how satellite imagery works and how to use it in your next Mapbox project.

![satellite imagery of Cyclone Debbie](/help/img/satellite/cyclone-debbie.jpg)

<div class='caption' markdown='1'>
Imagery of Tropical Cyclone Debbie off the coast of Australia in the spring of 2017.
</div>

## How satellite imagery works

Our satellite imagery comes from a variety of sources as raster data and is processed and composited together by Mapbox.

### Raster data

All satellite imagery is stored in raster format. Rasters are a [pixel-based data format](http://en.wikipedia.org/wiki/Raster_graphics) that efficiently represent continuous surfaces. Information in a raster is stored in a grid structure with each unit of information, or pixel, having the same size and shape but varying in value. Digital photographs, orthophotography, and satellite images are all stored in this format.

![rasters-are-pixels](/help/img/satellite/rasters-are-pixels.png)

Raster formats are well-suited to analyses that look at change over space and time because each data value has an accessible location based on the grid. This allows us to access the same geographic location in two or more different rasters and compare their values.

### Satellite rasters

When Earth-observing satellites take a picture, they read and record reflectance values collected from wavelengths along the electromagnetic spectrum.

![diagram of electromagnetic spectrum](/help/img/satellite/rasters-emspectrum.png)

<div class='caption' markdown='1'>
**Source**: Comparison of wavelength, frequency and energy for the electromagnetic spectrum.” Digital image. The Electromagnetic Spectrum. March 2013. Accessed June 2017. [https://imagine.gsfc.nasa.gov/science/toolbox/emspectrum1](https://imagine.gsfc.nasa.gov/science/toolbox/emspectrum1.html).
</div>

<!--copyeditor ignore previously-->
The human eye can only see a small part of the light-energy that is the [electromagnetic spectrum](http://en.wikipedia.org/wiki/Electromagnetic_spectrum). This is called _visible light_, because our vision evolved to be most sensitive where the sun emits the most light, and is broadly restricted to wavelengths that make up what we call red, green, and blue. Satellite sensors perceive a far wider range of the electromagnetic spectrum. The ability of sensors to collect information outside of our normal range of vision allows us to make visible the previously invisible.

The electromagnetic spectrum has such a wide range it would be impractical for a sensor to collect information from all wavelengths at the same time. Instead, different sensors prioritize the collection of information from different wavelengths of the spectrum. Each section of the spectrum that is captured and categorized by a sensor is categorized as a *band* of information.

Bands of information vary in size and can be compiled into different types of composite images, each emphasizing a distinct physical property. Mapbox Satellite imagery primarily relies on bands 1, 2, and 3 which make up visible red, green, and blue visible light.

### Satellite sources

Mapbox Satellite imagery comes from a [variety of sources](https://www.mapbox.com/about/maps/#data-sources) depending on zoom level and geographic availability:

- **Zoom levels 0-8** use [de-clouded](https://www.mapbox.com/blog/improving-mapbox-satellite-by-making-clouds-disappear/) data from NASA MODIS satellites.
- **Zoom levels 9-12** use [NASA/USGS Landsat 5 & 7](https://www.mapbox.com/blog/open-aerial/) imagery.
- **Zoom levels 13+** use a combination of open and proprietary sources, including [Digital Globe](https://www.mapbox.com/blog/digital-globe-partnership/) for much of the world, USDA’s NAIP 2011–2013 in the contiguous United States, and open aerial imagery from Denmark, Finland, and parts of Germany.

This layer is optimized for a balance between recency and aesthetic quality depending on data availability.

Before it's added to Mapbox Satellite, all our imagery is color-corrected, optimized, and composited together into a single raster tileset by our Satellite team. For a brief introduction to what this process involves, read our [Processing satellite imagery](/help/tutorials/processing-satellite-imagery) tutorial.

While Mapbox Satellite focuses on showing the clearest imagery at the highest resolution possible, we also offer our [Landsat Live](/help/glossary/landsat-live) basemap with the _latest_ global imagery. Landsat Live imagery comes from NASA's Landsat 8 satellite and is captured within the past 16 days. Our live pipeline sources this data from the [Landsat on AWS public dataset](https://aws.amazon.com/public-datasets/landsat/) and has global coverage. Explore our [live Landsat tool](https://www.mapbox.com/bites/00145/#8/39.996/25.131) to see when and where imagery was last refreshed.

## Using satellite imagery

Mapbox satellite is a composite imagery layer with global coverage to zoom 16 (1-2m resolution), regional coverage to zoom 18 (0.6-0.3m resolution), and select coverage to zoom 21+ (7.5cm+). There are several ways you can use Mapbox Satellite in your projects:

- Add it as a template style in [Mapbox Studio](https://www.mapbox.com/studio-manual/reference/styles/#pick-a-template).
- [Add Mapbox Satellite as a layer in Mapbox Studio](https://www.mapbox.com/studio-manual/reference/styles/#new-layer).
- Use Mapbox Satellite through any of [Mapbox's APIs and SDKs](https://docs.mapbox.com) with the tileset ID `mapbox.satellite`.
- Add Landsat Live imagery to your project using the tileset ID `mapbox.landsat-live`.

### Uploading satellite imagery

If you have access to imagery that better meets your needs than our Satellite layer, you can upload it using the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) or through your [Mapbox Studio](https://www.mapbox.com/studio) account. Make sure you convert your imagery into [GeoTIFF](/help/glossary/tiff) format before you upload. Once you've uploaded your data, it will be automatically converted into a custom raster tileset which you can then add to your Mapbox project. For more information on uploading satellite imagery, see our [Processing satellite imagery](/help/tutorials/processing-satellite-imagery/) tutorial.

### Tracing satellite imagery

Mapbox grants users a license to trace imagery for OpenStreetMap. Producing derivative vector tilesets from imagery for commercial purposes requires is only permitted under a Mapbox Commercial Satellite license. [Contact our sales team](https://www.mapbox.com/contact/sales/) for more information.

## Providing satellite feedback

If you notice an area where imagery needs improvement or updates for any reason, let us know by leaving your feedback with our [imagery request tool](https://www.mapbox.com/imagery-requests). This tool adds your requests to a master list that we consult when prioritizing updates. If you wish to recommend an imagery source, please mention it in your request. Please note that imagery is not improved on a set schedule and is updated when and where it becomes available.
