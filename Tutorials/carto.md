---
title: Add a Mapbox style to a CARTO map
description: Add your map as a basemap to CARTO.
thumbnail: carto
level: 1
topics:
- third party integration
language:
- No code
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: tutorial
---

<!--copyeditor disable basemap-->

Maps styles created with the [Mapbox Studio](https://www.mapbox.com/studio) style editor or [Studio Classic](https://github.com/mapbox/mapbox-studio-classic) can be added as basemaps to CARTO. Any of the preset basemaps or a custom style from Mapbox can be added as the primary basemap for your CARTO map.

## Getting started

For this guide, you'll need a Mapbox account and a CARTO account. Log in to each, then head on to the next steps.

Open the CARTO project where you would like to add your Mapbox style. Click on the pencil icon and click on the current **BASEMAP** that is listed.

<img alt='CARTO change basemap dialog' src='/help/img/3rdparty/cartodb-change-basemap.png' class='block wmax600 mx-auto'>

Under _Style_, click the **+** .

<img alt='Add a style in CARTO' src='/help/img/3rdparty/cartodb-add-style.png' class='block wmax600 mx-auto'>

## Add style created with Studio

In Mapbox Studio, click the **Share &amp; use** button next to the style you would like to add to your CARTO project.

![Mapbox style share and use modal](/help/img/3rdparty/cartodb-style-share.png)

When the **Share &amp; use** modal opens, switch to the **Use** tab. Click the **Third party** option, and toggle to **CARTO**. Copy the URL by clicking the {{<Icon name='clipboard' inline={true} />}} clipboard icon.

<img alt='Mapbox style Use modal CARTO item' src='/help/img/3rdparty/cartodb-share-page.png' class='block mx-auto'>

Back in CARTO, paste the Share URL you copied in the previous step into the text box, then click on **ADD BASEMAP**.

![CARTO add basemap dialog](/help/img/3rdparty/cartodb-add-studio-xyz.png)

The Studio style you added will appear as the CARTO basemap.

## Add style created with Studio Classic

In Mapbox Studio, visit the Classic page at [mapbox.com/studio/classic](https://www.mapbox.com/studio/classic/) . Find the style you would like to use, then click on the clipboard icon {{<Icon name='clipboard' inline={true} />}} to copy the style's tileset ID to your clipboard.

Head back to your CARTO project, where the "Change basemap" dialog should still be open. Click on the **Mapbox** tab, and paste the tileset ID you copied to your clipboard in the previous step into the "Enter Your Map ID/URL" text box. You will also need to paste a valid [access token](https://www.mapbox.com/account/access-tokens) into the "Enter Your Access Token" text box. To finish adding your Mapbox basemap, click on **ADD BASEMAP**.

![CARTO add Mapbox map dialog](/help/img/3rdparty/cartodb-add-classic.png)

The Mapbox Studio Classic style you  added will appear as the CARTO basemap.

## Finished product

You added styles created in both Mapbox Studio and Mapbox Studio Classic to a map in CARTO!
