---
title: Processing satellite imagery
description: Learn how to find satellite raster data, process it using the Rasterio command-line tool, and publish it on a webpage.
thumbnail: processingSatelliteImagery
level: 3
topics:
- analysis
- satellite
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

In this tutorial, you will learn how to find satellite raster imagery, then use command line tools to process these images. Finally, you will use Mapbox GL JS to create a map that demonstrates how Dubai's landscape has changed from the early 2000s to the present.

To do this, you will use imagery from the USGS Landsat satellites to create georeferenced composite images using the red, green, and blue bands to prioritize the natural look of land and water. Landsat imagery is free to use, and is typical of what you often see in other resources.

{{
  <DemoIframe src="/help/demos/processing-satellite-imagery/index.html" />
}}

## Getting started
If you are new to working with satellite imagery, or are unfamiliar with bands or the raster data type, read the [How satellite imagery works guide](/help/how-mapbox-works/satellite-imagery) before getting started.

There are a few tools you will need to complete this tutorial:

- **GDAL.** [GDAL](http://www.gdal.org/) is a low-level GIS toolkit that Rasterio depends on. Install GDAL using the method recommended for your operating system.
- **Rasterio.** [Rasterio](https://github.com/mapbox/rasterio) is a tool for reading and writing geospatial raster data. Install Rasterio on the command line with the command `pip install rasterio`.
- **NASA Earthdata account**. A free [NASA Earthdata account](https://urs.earthdata.nasa.gov/users/new) will let you use [EarthExplorer](https://earthexplorer.usgs.gov), where the data for this tutorial comes from.
- **Your Mapbox access token.** You can find your access token on your Mapbox [Account page](https://www.mapbox.com/account/).
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.

You will also need to be familiar with how to use the command line to complete this tutorial.

## Download scenes from EarthExplorer

<!--copyeditor disable cut-->
Landsat image data is cut into **scenes**, which are roughly square images, for distribution. You can think of a scene as a single frame from a camera. A Landsat scene covers about 170 &times; 185 kilometers (105 &times; 115 miles).

{{
    <Note
        title="Landsat's imaging process"
        imageComponent={<BookImage />}
    >
        <p>For a more detailed understanding of Landsat's imaging process, see the <a href='https://directory.eoportal.org/web/eoportal/satellite-missions/l/landsat-8-ldcm'>Landsat Data Continuity Mission documentation</a>.</p>
    </Note>
}}

In this tutorial, you will compare historical and present-day scenes of Dubai in the United Arab Emirates that show the landscape before and after Dubai's period of economic growth in the early 2000s. To make this comparison, the scenes in this tutorial come from two different satellites in the Landsat series. The "before" image is from Landsat 5, which was decommissioned in 2013, and the "after" image is from Landsat 8, the latest satellite. Some features change between these satellites, but in general the Landsat program maintains as much consistency as possible, which makes this kind of comparison possible.

Before you begin, create a new folder to keep your project files in. The instructions below reference specific Landsat scenes, but you can choose any scenes that you prefer.

### Download the Landsat 5 scene
1. Log in to [EarthExplorer](http://earthexplorer.usgs.gov) with your Earthdata account.
1. In the **Search Criteria** tab, type "Dubai" in the **Address/Place** search bar. Click the **Show** button, then select the result.
1. Click on the **Data Sets** tab.
1. Drill down to the _Landsat 4-5 TM C1 Level-1_ data set by clicking on **Landsat**, then **Landsat Collection 1 Level-1**.
1. Click the checkbox next to _Landsat 4-5 TM C1 Level-1_ to select it.
1. Click on the **Additional Criteria** tab.
1. Paste the following ID into the _Landsat Product Identifier_: `LT05_L1TP_160043_20011208_20180930_01_T1`.
1. Click the **Results** button.
1. Click the download icon under the resulting data product (the green arrow pointing down), then click the **Download** button next to the _Level-1 GeoTIFF Data Product_ option.
1. Save the file to your project folder.

### Download the Landsat 8 scene
1. Go back to the **Data Sets** tab and click on the checkbox next to the _Landsat 4-5 TM C1 Level-1_ data set to deselect it.
1. Click the checkbox next to _Landsat 8 OLI/TIRS C1 Level-1_ to select it.
1. Click on the **Additional Criteria** tab.
1. Paste the following ID into the _Landsat Product Identifier_: `LC08_L1TP_160043_20181207_20181211_01_T1`.
1. Click the **Results** button.
1. Click the download icon under the resulting data product (the green arrow pointing down), then click the **Download** button next to the _Level-1 GeoTIFF Data Product_ option.
1. Save the file to your project folder.

### Examine the bundle contents

The Landsat Level 1 products that you downloaded are compressed `.tar.gz` files called *bundles*. Unpack both bundles. The method you use to unpack them will vary depending your computer's operating system, or your web browser may unzip or fully unpack them automatically. As long as the unpacked bundles are directories in your project folder, you will be able to follow the processing instructions exactly.

Each bundle will unpack into a directory that contains 14 items, mostly TIFF images. Each item's name starts with the Landsat product ID and ends with the band number. For example, `LT05_L1TP_160043_20011208_20180930_01_T1_B1.TIF` is the Band 1 readout for the Landsat 5 `LT05_L1TP_160043_20011208_20180930_01_T1` scene.

Open `LT05_L1TP_160043_20011208_20180930_01_T1_B1.TIF` to see what Band 1 for the Landsat 5 scene looks like.

{{
<AppropriateImage imageId="processingSatelliteImageryL5B1" alt="A screenshot of the file LT05_L1TP_160043_20011208_20180930_01_T1_B1.TIF" />
}}

## Process Landsat 5 imagery

Now that you have the images you want, you will process them so that you can use them in a live map. You will work entirely from the command line for this section, starting with the Landsat 5 bundle you downloaded earlier.

In the following steps, you will composite the bands into a single image, reproject these bands into the Web Mercator (EPSG:3857) projection, then color-correct the image.

### Composite the bands
The aim of this tutorial is to make a visible image, and the natural choice would be to use the red, green, and blue bands to make a red, green, blue image. But Landsat 5 doesn’t have a blue band, so instead you will make a slightly false-color image with green for blue, red for green, and near-infrared for red. This wouldn’t work for scientific analysis, but it’s fine for visualization purposes.

The numbers of the Landsat 5 bands you’ll use, which will map respectively to red, green, and blue, are 3, 2, and 1. To stack those bands into an RGB image, you will use [`rio stack`](https://github.com/mapbox/rasterio/blob/master/docs/cli.rst#stack) to composite the TIFF files for Bands 1-3 and export them as a new file.

Copy and paste the following command into the command line:

```
rio stack --rgb LT05_L1TP_160043_20011208_20180930_01_T1/LT05_L1TP_160043_20011208_20180930_01_T1_B{3,2,1}.TIF landsat5_stack.tif
```

The `--rgb` option tells viewing software (for example Photoshop) that the bands should be interpreted as red, green, and blue.

The last argument in this command is the new output file (`landsat5_stack.tif`). The `LT05_L1TP_160043_20011208_20180930_01_T1_B{3,2,1}.TIF` argument specifies the files that get combined. This command uses a shell expansion to specify bands 3, 2, and 1 instead of separately naming each band file.

After the command runs, check your project folder. You will see the new `landsat5_stack.tif` file. Open this file to see what the new composite image looks like.

{{
<AppropriateImage imageId="processingSatelliteImageryLandsat5Stack" alt="A screenshot of the composited image file landsat5_stack.tif" />
}}

### Reproject the image

Next, you will reproject the composite image into the [Web Mercator (EPSG:3857)](https://en.wikipedia.org/wiki/Web_Mercator_projection#EPSG:3857) projection with [`rio warp`](https://github.com/mapbox/rasterio/blob/master/docs/cli.rst#warp). You will tell `rio warp` to reproject with bilinear sampling, a method that does not leave pixelation.

Copy and paste the following command into the command line:

```
rio warp --resampling bilinear --dst-crs EPSG:3857 landsat5_stack.tif landsat5_mercator.tif
```

The `--dst-crs EPSG:3857` option sets the projection to Web Mercator. The last argument in this command is the new output file (`landsat5_mercator.tif`).

After the command runs, open the new file with the reprojected image, `landsat5_mercator.tif`. It will look like the image in `landsat5_stack.tif` because the original projection is fairly close to Web Mercator.

{{
<AppropriateImage imageId="processingSatelliteImageryLandsat5Mercator" alt="A screenshot of the reprojected image file landsat5_mercator.tif" />
}}

### Color-correct the image

Next, you will change the color, saturation, and contrast of the image using [`rio color`](https://github.com/mapbox/rio-color), a color-correction plugin for Rasterio. Remember that `rio color` will create a useful visualization, but not one that is suitable for analysis. For analysis, you would need a separate workflow that included top-of-atmospheric calibration and atmospheric correction.

Copy and paste the following command into the command line:

```
rio color landsat5_mercator.tif landsat5_color.tif gamma g 1.7 gamma r 1.4 sigmoidal rgb 10 0.4
```

This command applies a gamma of 1.7 to the green band and a gamma of 1.4 to the red band, as well as [sigmoidal contrast](http://www.imagemagick.org/Usage/color_mods/#sigmoidal) to all bands. (If you’re curious, you can change the numbers (and operations) in the `rio color` command to see if you can make the image clearer or more attractive.)

Open the newly created `landsat5_color.tif` file. You have successfully processed the Landsat 5 image.

{{
<AppropriateImage imageId="processingSatelliteImageryLandsat5Color" alt="A screenshot of the reprojected image file landsat5_color.tif" />
}}

## Process Landsat 8 imagery

Next, you will process the Landsat 8 image.

The processing steps are much the same as the ones that you performed for the Landsat 5 image, with one important addition. Landsat 8 data is collected by a sensor that has a higher radiometric resolution than the sensor on Landsat 5. This means that Landsat 8 data comes in a 16 bit format, while Landsat 5 comes as 8 bit. Because Mapbox only accepts 8 bit resolution images, you need to convert your 16 bit Landsat 8 bands into 8 bit.

Run the following commands in the command line:

1. Composite the bands: `rio stack --rgb LC08_L1TP_160043_20181207_20181211_01_T1/LC08_L1TP_160043_20181207_20181211_01_T1_B{3,2,1}.TIF landsat8_stack.tif`
1. Reproject the image: `rio warp --resampling bilinear --dst-crs EPSG:3857 landsat8_stack.tif landsat8_mercator.tif`

Next, you will use `rio color` to convert the image to 8 bit format. You will also color-correct the image in the same step.

Copy and paste the following command into the command line:

```
rio color --co photometric=rgb --out-dtype uint8 landsat8_mercator.tif landsat8_color.tif sigmoidal rgb 20 0.2
```

Open the newly created `landsat8_color.tif` file. You have successfully processed the Landsat 8 image.

{{
<AppropriateImage imageId="processingSatelliteImageryLandsat8Color" alt="A screenshot of the color-corrected and resampled image file landsat8_color.tif" />
}}

## Build a map using Mapbox GL JS

Now that your images are processed and ready to upload, you will upload them to your Mapbox account as tilesets so you can use them in your project.

### Upload to Mapbox Studio

The following steps show how to upload your GeoTIFFs to Mapbox using the Mapbox [tilesets](https://studio.mapbox.com/tilesets/) page. You can also upload using the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) if desired.

1. Navigate to the [Tilesets](https://studio.mapbox.com/tilesets/) page.
1. Click the **New tileset** button.
1. A new window will open. Select the final Landsat 5 file (`landsat5_color.tif`), then click **Confirm**. The page will let you know when the file has been uploaded successfully.
1. Repeat these steps with the final Landsat 8 file (`landsat8_color.tif`).

The uploaded tilesets are listed on your [tilesets](https://studio.mapbox.com/tilesets/) page. Each tileset has its own [tileset ID](/help/glossary/tileset-id), which you can find by clicking the **Menu** option to the right of the listed tileset. The tileset ID allows you to reference a tileset when you use developer tools, such as Mapbox GL JS or the Mapbox iOS or Android SDKs.

### Compare tilesets with Mapbox GL JS

Next, you will use the tileset IDs from your Landsat 5 and Landsat 8 tilesets to build a map with Mapbox GL JS. This project uses the [Mapbox GL Compare](https://github.com/mapbox/mapbox-gl-compare) plugin to compare the Landsat 5 and Landsat 8 images.

1. Open your text editor and create a new file named `index.html`.
1. Copy and paste the code below into your text editor to initialize a Mapbox GL JS map.
1. Replace the `ACCESS_TOKEN` placeholder with your own Mapbox access token, which is on your [Account page](https://account.mapbox.com/).
1. Replace the `BEFORE_STYLE` placeholder with the tileset ID of your Landsat 5 tileset, which you can find on the [Tilesets](https://studio.mapbox.com/tilesets/) page by clicking the **Menu** option to the right of the tileset.
1. Replace the `AFTER_STYLE` placeholder with the tileset ID of your Landsat 8 tileset, which you can find on the [Tilesets](https://studio.mapbox.com/tilesets/) page by clicking the **Menu** option to the right of the tileset.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8' />
    <title></title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }
    </style>
</head>
<body>

<style>
body {
  overflow: hidden;
}

body * {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>
<script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-compare/v0.1.0/mapbox-gl-compare.js'></script>
<link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-compare/v0.1.0/mapbox-gl-compare.css' type='text/css' />

<div id='before' class='map'></div>
<div id='after' class='map'></div>

<script>
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

var beforeTileset = 'BEFORE_STYLE';
var afterTileset = 'AFTER_STYLE';

var beforeMap = new mapboxgl.Map({
  container: 'before',
  style: {
    version: 8,
    sources: {
      'raster-tiles': {
        type: 'raster',
        url: 'mapbox://' + beforeTileset,
        tileSize: 256
      }
    },
    layers: [{
      id: 'simple-tiles',
      type: 'raster',
      source: 'raster-tiles',
      minzoom: 0,
      maxzoom: 22
    }]
  },
  center: [55.1720, 25.0859],
  zoom: 11
});

var afterMap = new mapboxgl.Map({
  container: 'after',
  style: {
    version: 8,
    sources: {
      'raster-tiles': {
        type: 'raster',
        url: 'mapbox://' + afterTileset,
        tileSize: 256
      }
    },
    layers: [{
      id: 'simple-tiles',
      type: 'raster',
      source: 'raster-tiles',
      minzoom: 0,
      maxzoom: 22
    }]
  },
  center: [55.1720, 25.0859],
  zoom: 11
});

var map = new mapboxgl.Compare(beforeMap, afterMap, {});

</script>

</body>
</html>
```

Open the file in your browser. You will see your initialized Mapbox GL JS map displayed in the browser window. Drag the slider left and right to compare the difference in Dubai's landscape.

## Finished product

<!--copyeditor disable best-->

You found your own satellite imagery, processed it for the best visual impact, and created a display to visualize landscape change over time. You also learned how to use command-line analysis tools to process any kind of raster imagery you might want to use with Mapbox.

{{
  <DemoIframe src="/help/demos/processing-satellite-imagery/index.html" />
}}

## Next steps

To learn more, complete the [Georeferencing imagery](/help/tutorials/georeferencing-imagery/) tutorial, which walks you through a manual process for georeferencing imagery or raster data that doesn't already come with a geospatial reference system. You can also explore out the [Mapbox GL JS examples](https://www.mapbox.com/mapbox-gl-js/examples/) page for ideas about how to extend your web applications even further.
