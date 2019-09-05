---
title: Style a single country
description: Find and upload open source data to style in Mapbox Studio.
thumbnail: styleSingleCountry
level: 1
topics:
- uploads
- map design
language:
- No code
contentType: tutorial
prependJs:
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import { Video } from '../../components/video';"
  - "import StyleCreate from '../../video/style-single-country-style-create.mp4';"
---

<style>
    .color-swatch {
      width: 15px;
      height: 15px;
      border-radius: 15px;
      display: inline-block;
      margin-bottom: -2px;
    }
</style>

With the [Mapbox Studio](https://studio.mapbox.com) style editor, you can style a single country or region. In this example, you will be styling Australia.

## Getting started

Before getting started, you will need a few things:

- **Mapbox account**. You will need an account to log in and use the Mapbox Studio style editor. You can create an account at [mapbox.com/account](https://account.mapbox.com).
- **Natural Earth data**. Download the `Admin 0 - Countries` Shapefile from [Natural Earth](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/).

## Create a new style

Log into your Mapbox account and navigate to your [Styles](https://studio.mapbox.com/styles) page. This is where all your styles are listed. A [style](/help/glossary/style/) is a set of rules for how Mapbox will draw the map on a page – it includes references to your data, map images (icons, markers, patterns), fonts, and defines how all your data should be styled on your map. For more about styles, see the [Styles](https://docs.mapbox.com/studio-manual/reference/styles/) section of the Mapbox Studio Manual.

To create a new style from your [Styles](https://studio.mapbox.com/styles) page, click **New style**, scroll down, select **Blank**, and click **Customize Blank**. The style editor will automatically open.

{{
  <Video
    filename={StyleCreate}
    title="Create a new style modal in Mapbox Studio"
  />
}}

## Use the style editor

Use the style editor to add the data you downloaded to the map and adjust the style of the country.

### Add a tileset source

You can add Australia to the empty map canvas by uploading the Natural Earth data as a tileset:

1. Click **+ Layer**.
2. In the list of _Data sources_, click **+ Upload**, and select the Natural Earth data.
3. A popover will appear in the bottom right showing the progress of your upload.
4. Once the upload has "Succeeded", the tileset will be ready to use!
5. Search for your tileset in the _Data sources_ list and click the source and then the source layer you'd like to use.

The tileset you created includes all countries. To filter to use only Australia:

1. Click the **Filter** option and click **+ Create filter**.
2. Choose **NAME** from the list of data fields.
3. Type `Australia` into the search bar. Click **+ Use Australia** and then click **Done**.

{{
  <AppropriateImage
    imageId="styleSingleCountryFilter"
    alt="screenshot of how to filter data in the Mapbox Studio style editor"
  />
}}

4. In the original panel, flip back to the **Style** tab.
5. You'll see a black outline of Australia in your map canvas.

{{
  <AppropriateImage
    imageId="styleSingleCountryNoStyle"
    alt="screenshot of unstyled country"
  />
}}

### Style data

Next, click the **Style** tab to customize the look and feel of the layer. Change both the **Color** and **1px stroke** fields to {{<span className="color-swatch" style={{ backgroundColor: "#11b1f0" }}></span>}} `#11b1f0`.

{{
  <AppropriateImage
    imageId="styleSingleCountryFillColor"
    alt="screenshot of style panel in Mapbox studio"
  />
}}

### Publish

When you have finished editing your map style, publish your changes by clicking **Publish** in the upper right of the style editor. When you click the publish button, a window will display the difference between the previous and current version of this style. If you're happy with the changes, click **Publish**. Your style will now be available to share from a variety of tools and applications.

## Final product

You've styled a single country with the help of an outside data source. Mapbox Studio provides a wide variety of ways to use your new map style. You can use this map directly on your website or in a web or mobile application. Take a look at the [Publish style section](https://docs.mapbox.com/studio-manual/overview/publish-your-style/) of the Mapbox Studio Manual to see all the ways you can use your style!

## Next steps

Learn more about what you can do with the Mapbox Studio style editor in the [Mapbox Studio Manual](https://docs.mapbox.com/studio-manual/reference/styles/).
