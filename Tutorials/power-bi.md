---
title: Create data visualizations with the Mapbox Visual for Power BI
description: Use Microsoft Power BI to create a custom data visualization.
thumbnail: powerBi
level: 2
topics:
- third party integration
language:
- No code
prereq: Familiarity with Microsoft Power BI.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

Create customizable heatmaps, point cluster maps, and graduated circle maps with the **Mapbox Visual for Power BI** using Microsoft Power BI Desktop and Online. The Mapbox Visual can be imported and accessed as a visualization plugin inside Power BI. This guide will walk through getting started with the Mapbox Visual and how to create a Mapbox-powered visualization in [Microsoft Power BI](https://powerbi.microsoft.com/en-us/). You will need a Mapbox account and a Microsoft Power BI account to complete this tutorial.

![an interactive data visualization on a map](/help/img/3rdparty/power-bi-final-product.gif)

## Getting started

Here are a few resources you'll need before you get started:

- **Mapbox account**. You will need a Mapbox access token to add the Mapbox Visual in Power BI. Sign up for a free account on [Mapbox](https://account.mapbox.com/auth/signup/).
- **Power BI account**. Sign into your [Power BI account](https://app.powerbi.com/) or create a new one.
- **Mapbox Visual for Microsoft Power BI**. You can either add the Mapbox Visual using the Power BI Marketplace, or you can download the <a href='https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz'>latest Mapbox Visual</a> from the <a href='https://github.com/mapbox/mapboxgl-powerbi'>open-source GitHub repository</a>. Both of these options are explained in detail in the tutorial.
- **Data**. This guide uses a sample CSV file with US healthcare spending derived from [data.gov](https://catalog.data.gov/dataset/).

{{
<Button href="/help/data/power-bi-healthcare-spending.csv" passthroughProps={{ download: "power-bi-healthcare-spending" }} >
    <Icon name='arrow-down' inline={true} /> Download CSV
</Button>
}}


## Add data to Power BI

Start by adding data to a Power BI workspace.


{{<Note imageComponent={<BookImage />}>}}

This guide walks through using the Mapbox Visual in Power BI Online. The process in Power BI Desktop is similar, but the interface is different.

{{</Note>}}


### Add a new dataset

1. Sign into your Power BI account.
1. Click **Get Data** to import or connect to a data source.
1. To import the healthcare data you downloaded earlier, choose to _Import_ a _File_.
1. Choose _Local file_ and upload the CSV file.


{{<Note imageComponent={<BookImage />}>}}

You can use the _Mapbox Visual for Microsoft Power BI_ with any dataset that contains geographic longitude and latitude data values.

{{</Note>}}

![add a new data file to your Power BI account](/help/img/3rdparty/power-bi-add-data.png)

### Create a new report

In your Power BI workspace, navigate to the **Datasets** tab and create a new report by clicking the bar graph icon next to your new dataset. The report window will open and you will be able to edit your new report.

![create a new report in your Power BI workspace](/help/img/3rdparty/power-bi-create-workspace.gif)

### Add the Mapbox Visual to your Report

You'll add the Mapbox Visual using the _Visualizations_ pane:

1. In the _Visualizations_ pane, click the **Import a custom visual** option, represented by a three-dot icon.
1. Select **Import from marketplace**.
1. Enter "Mapbox" in the search menu and press enter.
1. Click the **Add** button next to the _Mapbox visual_ option to add it to your Power BI report. It will appear as a blue Mapbox logo on the _Visualizations_ toolbar.

{{<img alt='Screenshot showing the Mapbox Visual icon in the Visualizations pane in Power BI' src='/help/img/3rdparty/power-bi-choropleth-mapbox-visual.png' className='block wmax600 mx-auto' />}}

{{<Note title='Alternative workflow: Manual upload' imageComponent={<BookImage />}>}}

Alternatively, you can download the latest [Mapbox Visual for Power BI](https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz) from Mapbox's [open-source GitHub repository](https://github.com/mapbox/mapboxgl-powerbi):

1. Click the **Import a custom visual** icon (three dots) and select **Import from file**.
1. Upload the [latest Mapbox Visual](https://github.com/mapbox/mapboxgl-powerbi/raw/master/dist/mapboxGLMap.pbiviz).
1. A new blue Mapbox logo will appear in the _Visualizations_ pane.

{{</Note>}}

## Create a visualization

Click on the Mapbox icon in the _Visualizations_ pane to add a new visualization to your report. While customizing your visualization, you'll work in both the _Fields_ and _Format_ panels within the _Visualizations_ pane:

- The _Fields_ panel is where you will specify which data fields to associate with different types of Mapbox layers (for example map styles, heatmaps, circle maps, and cluster aggregation).
- The _Format_ panel is where you will specify the visualization style for each layer, such as color and radius.

### Initialize a visualization

In the _Fields_ panel, drag the `latitude` and `longitude` fields from your data onto the _Latitude_ and _Longitude_ shelves, and make sure that the _Do not summarize_ option is checked for both fields.  You should see the Mapbox visualization container populate with instructions on how to create your first visualization.

Connect your Mapbox account using your access token:

1. Click on the link, **Click here to get a free Mapbox access token**, in the visualization container.  Accept the external link request if prompted.  You will be forwarded to either the Mapbox sign up page or your Mapbox account page.
1. If you don’t have a Mapbox account, sign up with your email address.
1. Copy your Mapbox Access token from your [account page](https://www.mapbox.com/account/access-tokens).
1. Back in Power BI, go to the _Format_ panel and find the _Viz Settings_ option. Paste your access token in the _Access token_ field.

![animated GIF illustrating the process outlined above](/help/img/3rdparty/power-bi-initiate-viz.gif)

You will see your first map visualization!

![the resulting data visualization: a map with uniform circles at every point from the dataset](/help/img/3rdparty/power-bi-first-visualization.png)


### Change the map style

With the Mapbox Visual for Power BI, you can change the map style used in your visualizations. You can use any Mapbox default style or create a custom map style with Mapbox Studio. To update the map style:

1. In the _Format_ panel, select _Viz Settings_ > _Map Style_.
1. Select from any default map style. This example uses the Mapbox Satellite style.

{{<Note title='Custom map styles' imageComponent={<BookImage />}>}}
You can use any custom map style from your Mapbox Studio account by selecting **Custom style**. This is useful for adding custom polygons, drone imagery, or finely-tuning the context and design of your Mapbox visualization to help answer your business question.


When you select **Custom style**, you will be prompted to add a _style URL_. To learn how to find your custom style URL, read about more about [style URLs](/help/glossary/style-url).


To learn more about creating custom map styles in Mapbox Studio, explore the [Mapbox Studio manual](https://docs.mapbox.com/studio-manual/) or the [Create a custom map style](/help/tutorials/create-a-custom-style) tutorial. Have questions on how to implement these features? Reach out to our [support team](https://www.mapbox.com/contact/support).
{{</Note>}}

Now you'll see your data on top of a satellite map.

![the same data visualization as above, but with a satellite map behind the circle layer](/help/img/3rdparty/power-bi-viz-settings-map-style.png)

## Create a cluster layer

Next, you'll adjust the visualization to illustrate where the average covered costs are lowest in the US using a cluster layer.

In the _Fields_ panel, add the `Avg Covered Charges` field from your data to the _Cluster_ shelf.

In the _Format_ panel:

1. Turn the _Cluster_ layer **On** and the _Circle_ layer **Off**.
1. Under _Cluster_, select `maximum` from the _Aggregation type_ drop down list.

![animated GIF illustrating the process outlined above to add a cluster layer](/help/img/3rdparty/power-bi-cluster.gif)

### Style the cluster visualization

In the cluster _Format_ panel:

1. Change the _Min Color_ to `FEC0BF` and the _Max Color_ to `FF0027`.
1. Change the _Cluster Radius_ to `30`.
1. Set the _Blur_ to `0`.
1. Set the _Stroke Width_ to `3`.
1. Set the _Max Zoom_ to `6`.

![screenshot of the Power BI UI with the properties as specified above](/help/img/3rdparty/power-bi-cluster-styled.png)


## Update layers based on zoom level

Sometimes you may want to visualize data differently at different zoom levels. With the Mapbox Visual for Power BI, you can use multiple layers in a single visualization and specify at which zoom levels each layer should be displayed. Here, you'll show a cluster layer at low zoom levels (zoomed further out) and a circle layer at high zoom levels (zoomed further in).

### Add data properties to shelves

In the _Fields_ panel:

1. Add the `Average covered charges` data field to both the _Color_ and _Size_ shelves.
1. Add `Provider Id` to the _Tooltip_ shelf.

![screenshot of the Power BI UI with the properties as specified above](/help/img/3rdparty/power-bi-add-shelves.png)

### Style the circle layer

Then, in the _Format_ panel re-enable the circle layer by toggling the _Circle_ layer **On**, and update the style properties:

1. Set the circle _Radius_ to `1` and the _Zoom scale_ factor to `10`.
1. Set the circle _Min Color_ to `FEC0BF`, _Med Color_ to `FD817E`, and _Max Color_ to `FF0027`.
1. Set the circle _Stroke Color_ to white.
1. Set the circle _Min Zoom_ to `6`. This will hide the circle layer while the cluster visualization is being displayed.

![screenshot of the Power BI UI with the properties as specified above](/help/img/3rdparty/power-bi-update-on-zoom.png)

## Final product

You created a visualization in Microsoft Power BI using the Mapbox Visual for Power BI.

![an interactive data visualization on a map](/help/img/3rdparty/power-bi-final-product.gif)


## Next steps

For support and troubleshooting with the Mapbox Visual, you can open an issue in our [open source repository](https://github.com/mapbox/mapboxgl-powerbi) or [contact our support team](https://www.mapbox.com/contact/support/#other).

Want to do more with Mapbox and Power BI? [Contact sales](https://www.mapbox.com/contact/sales) to learn what else is possible &mdash; from adding custom shapes to visualize territories, adding detailed indoor maps, or visualizing billions of data points.
