---
title: Add a Mapbox Studio style as a basemap in ArcGIS Online
description: Add your map as a basemap to ArcGIS Online.
thumbnail: arcgisOnline
level: 2
topics:
- third party integration
language:
- No code
prereq: Familiarity with and access to ArcGIS Online.
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

Mapbox allows you to integrate your [Mapbox Studio styles](https://www.mapbox.com/studio/styles) with [ArcGIS Online](https://www.arcgis.com/home). In this tutorial, you'll learn how to add a style from your Mapbox account to your ArcGIS Online project as a tile layer.

## Getting Started

There are a few resources you will need to follow along with this tutorial:

- **ArcGIS Online account.** You can sign up for a free account on the [ArcGIS website](https://www.arcgis.com/home/createaccount.html).
- **Integration URL.** You can find the integration URL in the *Share &amp; use* modal for your [style](https://www.mapbox.com/studio). Finding this will be covered in a later step.

## Create a new project in ArcGIS

Navigate to your ArcGIS Online projects page and create a new project:

- Log into ArcGIS Online.
- Navigate to the [**Make a Map**](https://www.arcgis.com/home/webmap/viewer.html) page. This will automatically create a new project.
- Click **Add** > **Add Layer from Web**.

{{
  <AppropriateImage
    imageId="arcgisDropdown"
    alt="how to initialize adding a layer from web in ArcGIS"
  />
}}

A new window will open. Choose **A Tile Layer** from the dropdown list.

{{
  <AppropriateImage
    imageId="arcgisTileLayerBlank"
    alt="how to specify a tile layer in ArcGIS"
  />
}}

## Find your ArcGIS integration URL

In another tab in your browser, open Mapbox Studio and find your ArcGIS integration URL:

- Log into [Mapbox Studio](https://www.mapbox.com/studio).
- Open the style you would like to use in the style editor.
- Click on the **Share...** button in the top bar.
- When the **Share** modal opens, make sure you're looking at the **Production** tab.
- Toggle to the **Third party** option.
- Select the **ArcGIS Online** option in the drop down.
- Copy the URL by clicking the {{<Icon name='menu' inline={true} />}} clipboard icon.

{{
  <AppropriateImage
    imageId="arcgisSharePage"
    alt="Screenshot showing the Share modal in Mapbox Studio"
  />
}}

## Add your Mapbox style as a tile layer

Let's return to ArcGIS Online to finish adding our tile layer:

<!--copyeditor ignore basemap-->

- Navigate back to your ArcGIS Online project.
- In the open **Add Layer from Web** window, paste your ArcGIS integration URL in the **URL** field.
- Check the **Use as Basemap** box.
- Add a **Title** to your layer.
- Add "© OpenStreetMap contributors Design © Mapbox" to the **Credits** field.
- Click **Add Layer**.

{{
  <AppropriateImage
    imageId="arcgisTileLayerFilled"
    alt="complete add layer from web form in ArcGIS"
  />
}}

## Finished product

You've successfully added your Mapbox style as the basemap in your ArcGIS Online project.

<iframe width="500" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Mapbox and Esri" src="//www.arcgis.com/apps/Embed/index.html?webmap=9584661e8d7341bc8a6708defb704419&extent=-123.4323,45.1638,-121.8598,45.8605&zoom=true&previewImage=false&scale=true&disable_scroll=true&theme=light"></iframe>

## Next steps

If you're interested in creating a custom or branded style in Mapbox Studio to be used in ArcGIS Online, take a look at our [Create a custom style](/help/tutorials/create-a-custom-style) tutorial.
