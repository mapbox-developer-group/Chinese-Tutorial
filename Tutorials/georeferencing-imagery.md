---
title: Georeference imagery
description: Take your non-georeferenced aerial image or historical map and get it onto a Mapbox map with the help of QGIS.
thumbnail: georeferencingImagery
level: 3
topics:
- uploads
- satellite
- third party integration
language:
- No code
prereq: Familiarity with QGIS.
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

**Georeferencing** is the process of assigning geographic coordinates to a raster image to define its location in the world based on a map coordinate system. If you've ever used [Mapbox Satellite](/help/glossary/mapbox-satellite/) you've already worked with georeferenced images. This is because each raster tile in Mapbox Satellite is an image that's been assigned a particular location in the world.

There are lots of reasons why you may want to georeference your own custom raster images. For example, you might receive satellite imagery in a non-spatial image format, you may need to compare historic maps to current maps, or you might be building an interactive map of a fictional place for a gaming app.

For this tutorial, you'll be georeferencing a JPEG image of historical downtown Portland, Oregon using [QGIS](http://qgis.org/), a free open-source Geospatial Information System (GIS). Once you've exported your image to [GeoTIFF](/help/glossary/tiff/) format in QGIS, you'll upload it to your Mapbox account as a [tileset](/help/glossary/tileset/). Mapbox does not provide built-in tools to georeference your imagery because there are free, open-source tools that do this, such as QGIS.


![historical map of Multnomah county](/help/img/3rdparty/multnomah-county.png)


## Getting started

For this tutorial you'll need:

- **QGIS**. Follow the [download instructions](http://qgis.org/en/site/forusers/download.html) for more information and be sure you've installed the latest version.
- **An image to georeference**. This tutorial uses a historical map of downtown Portland, Oregon in JP2 (a type of high resolution JPEG) format, which you'll need to download. This image is clipped from a [larger map of Multnomah County, Oregon](https://www.loc.gov/resource/g4293m.la000694/) provided by the [Library of Congress](https://www.loc.gov/).{{<sup className='text-sup txt-s'>1</sup>}}

{{
<Button href="/help/data/downtown-pdx.jp2" passthroughProps={{ download: "downtown-pdx" }} >
    <Icon name='arrow-down' inline={true} /> Download image
</Button>
}}

## Georeference your image in QGIS

First you'll need to follow the instructions in the [Georeferencing Topo Sheets and Scanned Maps](http://www.qgistutorials.com/en/docs/georeferencing_basics.html) tutorial for QGIS. This introduction to georeferencing will guide you through the process using the most recent version of QGIS. Make sure you use the image you downloaded at the beginning of this tutorial rather than the image provided in the QGIS tutorial and `EPSG:900913` or `EPSG: 3857` (Web Mercator) as your coordinate reference system (CRS).

Once you've finished georeferencing your image, make sure to save your GeoTIFF file as **downtown-pdx.tif** in a convenient location for when you upload it to Mapbox.

## Upload to Mapbox as a tileset

You successfully transformed a JP2 image into a GeoTIFF and are ready to upload it to Mapbox as a tileset.

You can upload your GeoTIFF in [Mapbox Studio](https://www.mapbox.com/studio) or programmatically using the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads). For more information on uploading using Mapbox Studio, read the [Uploads](https://www.mapbox.com/studio-manual/overview/geospatial-data/) section of the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/). For more information on using the Uploads API, read the [Uploads API documentation](https://docs.mapbox.com/api/maps/#uploads).

## Finished product

You georeferenced your custom imagery and uploaded it to your Mapbox account. Now that your imagery is in raster tile format, you can add it to any of your Mapbox projects as a raster tile source. Here's an example of adding your imagery to a map using Mapbox GL JS.

{{
  <DemoIframe src="/help/demos/georef/index.html" />
}}

## Next steps

To learn more about georeferencing, read QGIS's advanced [Georeferencing Aerial Imagery](http://www.qgistutorials.com/en/docs/advanced_georeferencing.html) guide to extend your georeferencing skills.

---

{{<span className='txt-s'><sup className='text-sup'>1</sup> Habersham, Robert A, and Julius Bien & Co. Map of Multnomah County, Oregon: compiled from county records, railroad surveys, and other official data. [New York: Julius Bien & Co Photo. Lith, 1889] Map. Retrieved from the Library of Congress, https://www.loc.gov/item/2012586242/. (Accessed April 18, 2017.)</span>}}
