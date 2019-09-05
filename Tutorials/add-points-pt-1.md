---
title: "Add points to a web map, Part 1: create a dataset"
description: Create a new dataset containing points.
thumbnail: addPointsPt1
level: 1
topics:
- uploads
- datasets
- geocoding
language:
- No code
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

This tutorial is the first in a [series of tutorials](https://www.mapbox.com/studio-manual/help/#add-points-to-a-map) that will teach you how to add points to a map using the Mapbox Studio dataset editor, the Mapbox Studio style editor, and Mapbox GL JS.

*Part 1* of the series focuses on the Mapbox Studio dataset editor. In this tutorial, you will learn how to:

- Upload geospatial data as a dataset
- Draw additional data in the dataset editor
- Save and export your dataset as a tileset

{{
  <DemoIframe src="/help/demos/add-points-to-a-map/index.html" />
}}

## Getting started

There are a few resources you will need to follow along with this guide:

- **Mapbox account**. Sign up for a free account on [Mapbox](https://account.mapbox.com/auth/signup/).
- **Data**. Download this GeoJSON file, which includes the coordinates and feature properties for nine different Chicago Parks.

{{
<Button href="/help/data/chicago-parks.geojson" passthroughProps={{ download: "chicago-parks.geojson" }}>
    <Icon name='arrow-down' inline={true} /> Download GeoJSON
</Button>
}}

## Upload a new dataset

You can store an editable version of your data in your Mapbox account by uploading it to Mapbox Studio as a _dataset_. Having an editable version of your data means that you can add, remove, and edit features (points, lines, and polygons) and properties for each feature.

{{
<Note
  imageComponent={<BookImage />}
>
  <p>If you don't need to edit or draw data from scratch, you can upload data to Mapbox as a <em>tileset</em> instead of a <em>dataset</em>. For more information on the difference between tilesets and datasets, see the <a href='https://www.mapbox.com/studio-manual/overview/geospatial-data/'>Uploads section</a> of the <a href='https://www.mapbox.com/studio-manual/'>Mapbox Studio Manual</a>.</p>
</Note>
}}

### Create a dataset

1. Log into [Mapbox Studio](https://www.mapbox.com/studio) and navigate to the [Datasets page](https://www.mapbox.com/studio/datasets).
1. Click the **New dataset** button.
1. Select the **Upload** option in the upper right corner of the _New Dataset_ modal.
1. Select the GeoJSON file you downloaded. Click **Confirm**, then click **Create**.
<img src='/help/img/studio/point-tutorial-dataset-upload.png' alt='Screenshot illustrating how to create a dataset in Mapbox Studio' class='block wmax600 pt18 mx-auto'>
1. Once your file has completed uploading, click **Start editing**. The dataset editor automatically opens, and the data is displayed on a dark base map to help visualize the features.

![Screenshot showing the Mapbox Studio dataset editor](/help/img/studio/point-tutorial-dataset-editor.png)

### About datasets

You can edit both dataset features and properties in the dataset editor:

- **Features** are the points, lines, and polygons on your map. You can add new features using the draw tools, edit the placement or shape of features using by clicking and dragging features on the map, or remove features all together by clicking on them and hitting the delete key. You can also click on each feature in the dataset editor to view its properties.
- **Properties** can be strings, numbers, or boolean. In the sample dataset you uploaded, there are `title` and `description` properties for each point with a unique text string. You can edit properties, add new properties, or delete properties in the dataset editor. *Make sure any content that you want to display in popups in your final product is included as a property while you are working in the dataset editor.*

## Draw data

You can use the draw tools in the dataset editor to add a new point to your dataset. You can also change the geometry, placement, and properties of existing features with the dataset editor’s draw tools. Read more about draw tools in the [Mapbox Studio manual](https://www.mapbox.com/studio-manual/).

### Draw a new feature

1. Click inside the **Search places** field in the upper right side of the editor and search for `Garfield Park Chicago`.
1. Use the {{<Icon name='marker' inline={true} />}} draw tool to create a new point on the map at that location.
1. Next, click the **Add Property** button. Use the properties list on the left side of the screen to add the following field name and description:
  - Add the field name `title` and give it the value `Garfield Park`. Click **Confirm**.
  - Add the field name `description` and give it the value `Home of the Garfield Park Conservatory`. Click **Confirm**.

![animated GIF illustrating how to draw a new feature](/help/img/studio/point-tutorial-dataset-edit.gif)

## Export the dataset as a tileset

Next, you will save and export the dataset as a tileset so that you can add it to a Mapbox style.

### Create a tileset

1. Click the **Save** button in the upper right corner of the editor to save your changes.
1. Click the **Export** button, then select _Export to a new tileset_.
1. Name your tileset `chicago-parks` and click **Export**.
<img src='/help/img/studio/point-tutorial-export-to-tileset.png' alt='Screenshot illustrating how to export a dataset to a tileset in Mapbox Studio' class='block wmax600 pt18 mx-auto'>
1. After your tileset has successfully uploaded, click the tileset's name in the _Notifications_ pane to open it.

<img src='/help/img/studio/point-tutorial-tileset-upload.png' alt='Screenshot illustrating a successful tileset upload in Mapbox Studio' class='block wmax600 mx-auto'>

### About tilesets

Web maps are comprised of [map tiles](/help/how-mapbox-works/web-apps/). A collection of tiles is called a tileset. Mapbox cuts up data into tiles that are then added to a web map and displayed at various zoom levels. To make Mapbox maps more performant, a dataset's features are simplified when it is converted into a tileset.

## Next steps

Next, start [part 2](/help/tutorials/add-points-pt-2/) of this tutorial series to learn how to add your tileset to a map style in the Mapbox Studio style editor.
