---
title: Make a choropleth map with the Mapbox Visual for Power BI
description: Create a choropleth data map with the Mapbox Visual for Microsoft Power BI.
thumbnail: powerBiChoroplethMap
topics:
- third party integration
level: 2
language:
- No code
prereq: Familiarity with Microsoft Power BI.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Button from '@mapbox/mr-ui/button';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

In this tutorial, you will use the Mapbox Visual in [Microsoft Power BI](https://powerbi.microsoft.com/en-us/), data with information about US wildfires by state, and a custom tileset with information about US wildfires by county to create a choropleth visualization. This choropleth will display the number of acres burned at both the state and county levels, allowing you to drill into the data at the appropriate level. You will need a Mapbox account and a Microsoft Power BI account to complete this tutorial.

![A screenshot of a choropleth visualization in Power BI](/help/img/3rdparty/power-bi-choropleth-final.png)

{{
<Note
  imageComponent={<BookImage />}
>
  <p>This guide walks through using the Mapbox Visual in Power BI Online. The process in Power BI Desktop is similar, but the interface is different.</p>
</Note>
}}

## Getting started

Here are a few resources you'll need before you get started:

- **Mapbox account**. You need a [Mapbox account](https://account.mapbox.com/auth/signup/) and a Mapbox access token, which you can find on the [Account page](https://account.mapbox.com/).
- **Microsoft Power BI account**. Sign into your [Power BI account](https://app.powerbi.com/) or create a new one.
- **Mapbox Visual for Power BI**. You can either add the Mapbox Visual using the Power BI Marketplace, or you can download the <a href='https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz'>latest Mapbox Visual</a> from the <a href='https://github.com/mapbox/mapboxgl-powerbi'>open-source GitHub repository</a>. Both of these options are explained in detail in the tutorial.
- **Geospatial data.** You will upload this GeoJSON file, which contains county-level detail about wildfires in the United States, to Mapbox Studio as a tileset.

{{
<Button href="/help/data/power-bi-wildfires-by-county.geojson" passthroughProps={{ download: "power-bi-wildfires-by-county.geojson" }} >
    <Icon name='arrow-down' inline={true} /> Download GeoJSON
</Button>
}}

- **Dataset for Power BI**. You will upload this sample dataset, a CSV file that contains historical information about wildfires in the United States, to Power BI.

{{
<Button href="/help/data/power-bi-2014-widfires.csv" passthroughProps={{ download: "power-bi-2014-widfires" }} >
    <Icon name='arrow-down' inline={true} /> Download CSV
</Button>
}}

## Upload your tileset to Mapbox

Before you can reference the geospatial data from the downloaded GeoJSON file in a Power BI report, you need to upload it to Mapbox as a [tileset](/help/glossary/tileset/).

{{
<Note
  imageComponent={<BookImage />}
>
  <p>To upload geospatial data to Mapbox as a tileset, the data must be in one of the following formats:</p>
  <ul>
    <li>MBTile</li>
    <li>KML</li>
    <li>GPX</li>
    <li>GeoJSON</li>
    <li>Shapefile (zipped)</li>
    <li>CSV</li>
  </ul>
  <p>For information on upload file size limits for these formats, refer to the <a href="/help/troubleshooting/uploads/#tilesets">Uploads troubleshooting page</a>.</p>
</Note>
}}

1. Navigate to the [Tilesets page](https://www.mapbox.com/studio/tilesets/) in Mapbox Studio.
1. Click on the **New tileset** button.
![Screenshot showing the New tileset button in Mapbox Studio](/help/img/3rdparty/power-bi-new-tileset.png)
1. In the _New tileset_ window, you can either click the **Select a file** button and choose the file, or you can drag and drop the file directly into the window.
1. When you are prompted to do so, click **Confirm**.
![Screenshot showing the Confirm button in the New tileset window in Mapbox Studio](/help/img/3rdparty/power-bi-confirm-tileset-upload.png)
1. After the file uploads, you will see a confirmation success message. Click on the link in the confirmation message to open your new tileset’s information page. The tileset's information page includes the _tileset ID_, the layer's _name_, and the layer’s _properties_, all which you will need to reference in Power BI.

You will use these pieces of information in the [Add a custom tileset](#add-a-custom-tileset) section of this tutorial. For now, though, you will open Power BI.

## Add data to Power BI

You will start by adding the wildfire data you downloaded to a new Power BI workspace.

1. In Power BI, click **Get Data**, which allows you to import data or connect to a data source.
1. Under the _Files_ option, click **Get**.
1. Choose **Local File** and upload the wildfire data CSV file.

![A screenshot showing how to upload a CSV to Power BI](/help/img/3rdparty/power-bi-choropleth-upload.png)

{{
<Note
  title="Notes on using a custom dataset in Power BI"
  imageComponent={<BookImage />}
>
  <p>Your dataset should be a CSV file with at least 2 columns. One column must be a unique identifier, which will be used to match a unique property from your tileset. The second column must be the value you want to connect to the unique identifier. (For the dataset in this example, the unique property is the `state_name`, which you will match to the pre-defined Power BI state tileset. The value you connect to the unique identifier will be the number of acres burned.)</p>
</Note>
}}

## Create a new report
1. Click on **My Workspace** and select the **Datasets** tab.
1. Click the **Create a report** option (the bar graph icon) next to the new dataset. This will open the report window.

![A GIF showing how to create a new report in Power BI](/help/img/3rdparty/power-bi-choropleth-new-report.gif)

## Add the Mapbox Visual to the report

You can use the _Mapbox Visual for Microsoft Power BI_ with any dataset that contains geographic data values. To add the Mapbox Visual to your report:

1. In the _Visualizations_ pane, click the **Import a custom visual** option, represented by a three-dot icon.
1. Select **Import from marketplace**.
{{<img alt='Screenshot showing how to import a visual from marketplace in Power BI' src='/help/img/3rdparty/power-bi-choropleth-import.png' className='block wmax600 pt18 mx-auto' />}}
1. Enter "Mapbox" in the search menu and press enter.
1. Click the **Add** button next to the _Mapbox Visual_ option to add it to your Power BI report. After the Mapbox Visual is imported, it will appear as a blue Mapbox logo on the _Visualizations_ pane.

{{<img alt='Screenshot showing the Mapbox Visual icon in the Visualizations pane in Power BI' src='/help/img/3rdparty/power-bi-choropleth-mapbox-visual.png' className='block wmax600 mx-auto' />}}

{{
<Note
  title="Alternative workflow: Manual upload"
  imageComponent={<BookImage />}
>
  <p>Alternatively, you can download the latest <a href='https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz'>Mapbox Visual for Power BI</a> from Mapbox's <a href='https://github.com/mapbox/mapboxgl-powerbi'>open-source GitHub repository</a>:</p>
  <ol>
  <li>Click the <strong>Import a custom visual</strong> icon (three dots) and select <strong>Import from file</strong>.</li>
  <li>Upload the <a href='https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz'>latest Mapbox Visual</a>.</li>
  <li>A new blue Mapbox logo will appear in the <em>Visualizations</em> pane.</li>
  </ol>
</Note>
}}

## Build the choropleth visualization

### Include an access token

1. Click on the Mapbox icon in the _Visualizations_ pane to add a new visualization to your report.
1. In the **Fields** tab, drag the `state_name` field from your data onto the _Location_ shelf. You should see the Mapbox visualization container populate with instructions on how to create your first visualization.
{{<img alt='Screenshot showing the state_name field in the Location shelf' src='/help/img/3rdparty/power-bi-choropleth-state-name.png' className='mx-auto mt18' />}}
1. Connect your Mapbox account using your access token:
    - Click the **Click here to get a free Mapbox access token** link in the visualization container. Accept the external link request if prompted. You will be forwarded to either the Mapbox sign up page or your Mapbox account page.
    - Copy your Mapbox Access token from your [account page](https://www.mapbox.com/account/access-tokens).
  1. Back in Power BI, go to the **Format** tab and open the **Viz Settings** option. Paste your access token in the _Access token_ field.

{{<img alt='GIF showing how to add Mapbox access token in Power BI' src='/help/img/3rdparty/power-bi-choropleth-access-token.gif' className='block wmax600 mx-auto' />}}

### Create the choropleth

1. In the **Viz Settings** pane, change the _Map Style_ option to _Dark_.
1. Drag the `ACRES` field from the data options onto the _Color_ shelf.
1. Go back to the **Format** tab. Switch the **Circle** option off and turn the **Choropleth** option on.

You will see a choropleth that visualizes the number of acres burned per state.

![Screenshot showing the choropleth visualization in Power BI](/help/img/3rdparty/power-bi-choropleth-visualization-on.png)

### Add a custom tileset

To drill down more deeply into data about wildfires in the United States, you will reference the custom tileset with information about wildfires at the county level that you created in the first step of this tutorial.

To add this data to Power BI, you will plug its identifying features into the appropriate fields in Power BI. The information that you'll need from the tileset are the _tileset ID_, the _layer name_, and the _unique identifier property name_.

![Screenshot showing the elements necessary to add a tileset to Power BI: the tileset ID, the layer name, and the property name](/help/img/3rdparty/power-bi-tileset-details-pt2.png)

1. In the **Format** tab, click on **Choropleth** to open the choropleth layer settings.
1. Use the _Number of levels_ dropdown menu to change the number of levels to **2**. (Having two levels will allow you to drill down from the state-level data in Level 1 into the county-level data that you are adding now.)
1. In the _Level_ dropdown, select **Level 2**.
1. Click on the _Data Level 2_ dropdown.
1. Select the _Custom Tileset_ option.
{{<img alt='Screenshot showing how to add a custom tileset to a choropleth in Power BI' src='/help/img/3rdparty/power-bi-choropleth-custom-tileset.png' className='mx-auto mt18' />}}
1. In the _Vector Tile URL Level 2_ field, paste the tileset ID. The tileset ID in this field must always be preceded by `mapbox://`.
1. In the _Source Layer Name Level 2_ field, paste the layer's name.
1. In the _Vector Property Level 2_ field, enter the unique identifier property name: `id`.
1. Click on the **Fields** tab again. Drag the `county_id` field from the data options onto the _Location_ shelf.

{{
<AppropriateImage imageId="powerBiAddCustomTileset" alt="Screenshot showing how to add a Mapbox tileset ID, layer name, and property name in Power BI" />
}}

{{
<Note
  title="Using a custom tileset in Power BI"
  imageComponent={<BookImage />}
>
  <p>The boundaries in a custom tileset should contain one unique identifying property key that matches the dataset you are using in Power BI. Common examples are: FIPS code, zip code, ISO code, or any unique name string.</p>
</Note>
}}

## Final product

Use the buttons on the upper left side of the visualization to drill up to the state level or down to the county level. Hover over a state or county to see the number of acres burned in that specific boundary.

![Screenshot showing a county-level choropleth visualization in Power BI](/help/img/3rdparty/power-bi-choropleth-counties.png)

You have created a choropleth visualization in Microsoft Power BI using the Mapbox Visual for Power BI.

## Next steps

Explore ways to further customize the choropleth. For instance, you could use the **Choropleth** settings in the **Format** tab to change the color range of the visualization.

For support and troubleshooting with the Mapbox Visual, open an issue in the [open source repository](https://github.com/mapbox/mapboxgl-powerbi) or [contact our support team](https://www.mapbox.com/contact/support/#other).

Want to do more with Mapbox and Power BI? [Contact Mapbox sales](https://www.mapbox.com/contact/sales) to learn what else is possible, from adding custom shapes to visualize territories, adding detailed indoor maps, or visualizing billions of data points.
