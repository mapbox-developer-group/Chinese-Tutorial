---
title: Static and print maps
description: Learn how the Mapbox Static Images API works and how to create static maps.
image: /img/narrative/print.svg
topics:
  - print
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import { DemoStatic } from '../../components/demo-static';"
contentType: guide
---

Static maps are standalone images in PNG format that can be displayed on web and mobile devices without the aid of a mapping library or API. They look like an embedded map without interactivity or controls. You can request a static map from the Mapbox Static Images API by providing a few parameters, including center coordinates, zoom level, rotation, and tilt. Static maps may also include overlays like lines, markers, or polygons. **Learn how to build a Static Images API request using [the Static Images API playground](/help/interactive-tools/static-api-playground)**.

The image below was generated using the Mapbox Static Images API and can be added to a webpage using the following code:

```html
<img alt='static Mapbox map of the San Francisco bay area' src='https://api.mapbox.com/styles/v1/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}/static/-122.337798,37.810550,9.67,0.00,0.00/1000x600@2x?access_token={{ <UserAccessToken /> }}' >
```

{{
  <DemoStatic src="https://api.mapbox.com/styles/v1/mapbox/streets-v{constants.VERSION_STREETS_STYLE}/static/-122.337798,37.810550,9.67,0.00,0.00/1000x600@2x?access_token=MapboxAccessToken" alt="static mapbox map of the san francisco bay area" />
}}


## How static maps work

The Mapbox Static Images API allows you to request a static image representation of any map style in your Mapbox account. You can retrieve a static map in a few different image and file formats depending on the Mapbox tool you are using. See [How to create a static map](/help/how-mapbox-works/static-maps/#creating-static-maps) below for more information on supported file types.

### Retina

When you request a Retina map with `@2x`, you will receive an image that's twice the width and height that you've specified in your API call. For example, using a `width` attribute of 700&nbsp;px with the `@2x` parameter will return an image with an actual width of 1,400&nbsp;px.

### High resolution images

Mapbox Studio offers 100 high resolution image exports per account using the [print panel](https://docs.mapbox.com/studio-manual/reference/styles/#print-panel). If you are interested in having a higher number of allowed image exports, contact [Mapbox sales](https://www.mapbox.com/contact/sales).

With the Mapbox Static Images API, image exports can be up to 1,280&nbsp;px x 1,280&nbsp;px in size. While enabling retina may improve the quality of the image, you cannot export at a higher resolution using the Static Images API, and we do not support vector image formats.

### Static images for print

To print images generated from the Mapbox Studio print export option for any use, [contact us](https://www.mapbox.com/contact/sales/). Print maps require [appropriate Mapbox attribution](/help/how-mapbox-works/attribution#static--print).


## Creating static maps

Below is a list of image formats that are supported and which tools you can use to generate them:

Format | Tool(s)
-------|---------
PNG | [Mapbox Static Images API](https://docs.mapbox.com/api/maps/#static-images)
PNG, JPG<br>high-resolution | [Mapbox Studio](https://www.mapbox.com/studio-manual/reference/styles/#print-panel) (limited number of exports per account)

The following formats are **not supported** as a map export option and are not on our road map for integration:

* SVG
* EPS
* PDF

### Mapbox Static Images API

You can get a static image of your map by formatting a URL with your specific values to make the request. See the Mapbox [Static Images API documentation](https://docs.mapbox.com/api/maps/#static-images) for more information about available parameters and values.

### Mapbox Static Images API playground

To learn how to build a Static Images API request, explore [the Mapbox Static Images API playground](/help/interactive-tools/static-api-playground).

![screenshot of the Static Images API playground page](/help/img/interactive-tools/static-api-playground.png)

#### Overlays

You can add overlays to any maps made with the Static Images API. An overlay is data that can be added on top of the map at request time. Overlays are comma separated and can be a mix of valid GeoJSON, custom markers, paths, or polygons. Read more about how to add an overlay to a static map in our [Static Images API documentation](https://docs.mapbox.com/api/maps/#static-images).

### Mapbox Studio

The Mapbox Studio print panel allows you to export high resolution images of custom map styles. Click the {{<Icon name='printer' inline={true} />}} printer icon to toggle the print panel on and off. Position your map and specify **Print export settings** in the print panel. Settings include image dimensions (in inches or centimeters), resolution (in pixels per inch), and file format (PNG or JPG). The maximum image export is 8,000&nbsp;px by 8,000&nbsp;px.

Read more about the print panel in the [Mapbox Studio manual](https://www.mapbox.com/studio-manual/reference/styles/#print-panel).

![screenshot of the print panel with print export settings as described above](/help/img/studio/print-export-settings.png)
