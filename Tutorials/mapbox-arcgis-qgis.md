---
title: Add Mapbox maps as layers in ArcGIS and QGIS with WMTS
description: Learn how to add Mapbox maps as layers in ArcGIS and QGIS with WMTS.
thumbnail: mapboxArcgisQgis
level: 2
topics:
- third party integration
language:
- No code
prereq: Familiarity with and access to ArcGIS.
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

Mapbox provides many URLs and code snippets to help you add your custom Mapbox maps to other mapping tools. This tutorial will show you how you can add any Mapbox map as a layer in ArcMap or QGIS as WMTS.

## Getting started

Before diving in, make sure you have the following ready to go:

- **A Mapbox account**. If you haven't done so already, [sign up for a Mapbox account](https://www.mapbox.com/signup/).
- **ArcMap** or **QGIS** installed on your computer. You should be somewhat familiar with your mapping software's interface before starting this tutorial.
- **A Mapbox style**. Head to your [style page in Mapbox studio](https://www.mapbox.com/studio/styles/) to see a list of the styles in your account.

## Add Mapbox maps in ArcMap

ArcMap can read map tiles protocol, which is what you'll use to add your Mapbox styles. First, you will build a WMTS endpoint for the style you would like to add to ArcMap. Next, you will add this WMTS endpoint to your ArcMap project.

### Build a WMTS endpoint

The WMTS endpoint that you will use to add your map in ArcMap needs to follow this format:

```
https://api.mapbox.com/styles/v1/YOUR_USERNAME/YOUR_STYLE_ID/wmts?access_token={{ <UserAccessToken /> }}

```

There are three pieces of this URL that you will need to change:
1. **Mapbox username:** Replace "YOUR_USERNAME" with your Mapbox username, which you will find on your [Mapbox Studio homepage](https://www.mapbox.com/studio).
1. **Map style ID:** Replace "YOUR_STYLE_ID" with the style ID of the map you are adding to ArcMap. To find the style ID:
    - On your [Mapbox Studio homepage](https://www.mapbox.com/studio/), find the correct style from your list of styles.
    - Click the {{<Icon name="menu" inline={true} />}} **Menu** button.
    - Click the {{<Icon name="clipboard" inline={true} />}} icon to copy the Style URL, which will look like: `mapbox://styles/YOUR_USERNAME/YOUR_STYLE_ID`. The style ID is the last part of this URL.
1. **Mapbox access token:** Add your Mapbox access token, which you will find on your [Mapbox Account page](https://www.mapbox.com/account)).

When you have customized a WMTS endpoint with your username, the style ID, and your access token, it will be ready for you to use in ArcMap.

### Add your map in ArcMap

To get started in ArcMap:

1. Click the **Add Data** button in the toolbar to open the _Add Data_ dialog box.
2. At the top of the dialog box, click the arrow next to **Look in:** and select **GIS Servers**.

    ![ArcMap add data dialog](/help/img/3rdparty/arcgis-desktop-gis-servers.png)

3. Double-click **Add WMTS Server** to open the _Add WMTS Server_ dialog box.

    ![ArcMap add WMTS server dialog](/help/img/3rdparty/arcgis-desktop-add-wmts-server.png)

4. In the **URL** field at the top, paste the WMTS endpoint URL that you customized in the previous step.
5. In the _Server Layers_ section, click **Get Layers**. When prompted for a username and password, click **Cancel**. You may have to click it several times to dismiss the box.

    ![ArcMap add GIS server connection](/help/img/3rdparty/arcgis-desktop-gis-server-connection.png)

6. When the layers are loaded in the window, click **OK**.

    ![ArcMap add WMTS server confirmation dialog](/help/img/3rdparty/arcgis-desktop-server-layers.png)

7. You should see _Mapbox on api.mapbox.com_ in the **Add Data** dialog box. Double click it, select the name of your style in the next dialog box, then click **Add**.

    ![Mapbox style in ArcMap map preview window](/help/img/3rdparty/arcgis-desktop-streets-layer.png)

You should see your map as a layer inside your ArcMap project. Note that each style will have to be added individually.

## Add Mapbox maps in QGIS

QGIS can also read map tiles from a WMTS server. First, build a WMTS endpoint for the style you would like to add to QGIS. Next, add this WMTS endpoint to your QGIS project.

### Build a WMTS endpoint

The WMTS endpoint that you will use to add your map in QGIS needs to follow this format:

```
https://api.mapbox.com/styles/v1/YOUR_USERNAME/YOUR_STYLE_ID/wmts?access_token={{ <UserAccessToken /> }}

```

There are three pieces of this URL that you will need to change:
1. **Mapbox username:** Replace "YOUR_USERNAME" with your Mapbox username, which you will find on your [Mapbox Studio homepage](https://www.mapbox.com/studio).
1. **Map style ID:** Replace "YOUR_STYLE_ID" with the style ID of the map you are adding to QGIS. To find the style ID:
    - On your [Mapbox Studio homepage](https://www.mapbox.com/studio/), find the correct style from your list of styles.
    - Click the {{<Icon name="menu" inline={true} />}} **Menu** button.
    - Click the {{<Icon name="clipboard" inline={true} />}} icon to copy the Style URL, which will look like: `mapbox://styles/YOUR_USERNAME/YOUR_STYLE_ID`. The style ID is the last part of this URL.
1. **Mapbox access token:** Add your Mapbox access token, which you will find on your [Mapbox Account page](https://www.mapbox.com/account)).

When you have customized a WMTS endpoint with your username, the style ID, and your access token, it will be ready for you to use in QGIS.

### Add your map in QGIS

To add your Mapbox map to QGIS:

1. In QGIS, click the **Add WMS/WMTS** button.

    ![QGIS add layers from WMTS server dialog](/help/img/3rdparty/qgis-add-layer-from-server.png)

2. Make sure the _Layers_ tab is selected in the dialog box. Below the dropdown menu at the top of the box, click **New**.
3. Give the layer a name and add the WMTS endpoint URL that you customized in the previous step. Press **OK**.

    ![QGIS create a new WMS connection dialog](/help/img/3rdparty/qgis-create-wmts-connection.png)

4. Back in the _Add Layer(s) from a WM(T)S Server_ dialog box, the name of your layer should appear in the box at the top. When you see this, click **Connect**.

    ![QGIS layer confirmation dialog](/help/img/3rdparty/qgis-wmts-tileset.png)

5. The _Tilesets_ tab should open with a single layer. Select that layer and click **Add**, then click **Close** to close the dialog box.

    ![completed QGIS map with Mapbox style](/help/img/3rdparty/qgis-wmts-layer.png)

You should see your map as a layer inside your QGIS project. Note that any style you would like to visualize will have to be added individually.

## Finished product

You have used a WMTS endpoint to add a Mapbox style to your ArcMap or QGIS project.
