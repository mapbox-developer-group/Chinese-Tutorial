---
title: Create new data
description: Learn how datasets work and how to create geospatial data from scratch using Mapbox.
image: /img/narrative/data-create.svg
topics:
  - datasets
prependJs:
  - "import * as constants from '../../constants';"
  - "import { HmwDemo } from '../../components/hmw-demo';"
  - "import { datasetSample } from '../../snippets/dataset';"
contentType: guide
---

A **dataset** is an editable collection of [GeoJSON](/help/glossary/geojson/) [features](/help/glossary/features/). Unlike [tilesets](/help/glossary/tileset), datasets can be edited on a feature-by-feature basis. Datasets cannot be used directly in a Mapbox Studio style but can be exported as a tileset or rendered with Mapbox GL JS. Any dataset exported to a tileset can be added as a layer in the Mapbox Studio style editor.
<!--copyeditor ignore url-->
{{
    <HmwDemo
      visual={{
        title: "Mapbox Studio dataset editor",
        subtitle: "Use the dataset editor to create and manage your data",
        content: <div className='h300' style={{backgroundImage: "url(/help/img/studio/how-datasets-work.png)", backgroundSize: "cover"}}></div>
      }}
      code={{
        title: "Dataset",
        subtitle: "Sample GeoJSON FeatureCollection",
        content: <pre id='style-spec' className='txt-xs px12 mx0 my0 h300' style={{overflowY: "scroll"}}>
            {datasetSample}
        </pre>
      }}
    />
}}


In this example, you can see a visual representation of a dataset inside the **Mapbox Studio dataset editor** on the left and the actual contents of the **dataset**, a GeoJSON FeatureCollection, on the right. The contents of the dataset include geometry and properties for each point that you can see on the left, but does not contain any style information. For more details on how to style the points (for example, specify the symbols, colors, and the font for labels), see the [Upload data](/help/how-mapbox-works/uploading-data/) guide, which covers converting datasets to tilesets.


## How datasets work

Datasets are a hosted version of your raw data as **[GeoJSON](http://geojson.org/)**. You can access and edit your datasets with the dataset editor or the [Mapbox Datasets API](https://docs.mapbox.com/api/maps/#datasets).

### Format

<div class='fr pl12' style='width:50%'>
<pre>
{
    "id": "{feature_id}",
    "type": "Feature",
    "geometry": {
        "type": "Point",
        "coordinates": [0, 0]
    },
    "properties": {
        "name": "null island"
    }
}
</pre>
</div>

Datasets are stored as **[GeoJSON](http://geojson.org/)**, a format for encoding a variety of geographic data often used by Mapbox [web services and APIs](https://www.mapbox.com/developers/api/). Based on [JSON](http://www.json.org/) (JavaScript object notation), GeoJSON is native to the JavaScript language and can be parsed in modern software.

Mapbox stores dataset features as collections of GeoJSON features. Features are individual (or in some cases groups of) points, lines, or polygons. The Mapbox Datasets API does not support GeometryCollections or null geometries. Each feature is defined by its geometry and properties:

- **Geometry**: This describes the shape and the location of each feature. You can specify Points, LineStrings, Polygons. The location and the exact shape of each feature is determined by the coordinates that are specified.
- **Properties**: This can contain any JSON object. Some examples of common properties that are applied to Mapbox datasets include `title` and `description` to include in popups in a web application.

### Dataset to tileset process

You cannot add datasets directly to styles in the Mapbox Studio style editor. But you can export your dataset as a tileset and add it to your style in the Mapbox Studio style editor or Mapbox GL JS. When you export your dataset to a tileset, it is processed in the same way an upload would be processed.

You can read more about how raw data becomes a tileset in the [Upload data](/help/how-mapbox-works/uploading-data/) guide.

### Downloading datasets

Once you’ve created a dataset, you can export it to a tileset for use in a Mapbox map (see the [How map design works guide](/help/how-mapbox-works/map-design/) for more information), download it as a GeoJSON FeatureCollection, or access it with the Mapbox Datasets API. Datasets can still be edited after export, but you will need to make sure to sync your downloaded version with your new edits if you would like your local copy to reflect any changes you've made.

To learn how to download and export datasets, see the [datasets section of the Mapbox Studio Manual](https://www.mapbox.com/studio-manual/reference/datasets/).

## Creating datasets

You can create a dataset from scratch in the Mapbox Studio [dataset editor](https://www.mapbox.com/studio/datasets/) or through the [Mapbox Datasets API](https://docs.mapbox.com/api/maps/#datasets). Note that the process involves two steps in each case: creating an empty dataset, and adding features to that dataset.

### Mapbox Studio

In Mapbox Studio, you can use the dataset editor to create a new dataset using a visual interface rather than writing the GeoJSON directly. To create a dataset with the Mapbox Studio dataset editor, you can either create a new empty dataset and add features to it by drawing them in the dataset editor, or you can upload a GeoJSON or CSV file as a dataset and edit, add, and delete features using the dataset editor interface.

You can learn more about how to create datasets using the Mapbox Studio dataset editor in the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/reference/datasets/).

### Mapbox Datasets API

Using the Mapbox Datasets API, you can add features by making requests to [insert a feature](https://docs.mapbox.com/api/maps/#insert-or-update-a-feature). You cannot upload a file directly through the Datasets API. The Datasets API accepts one Feature at a time. If you would like to add many Features from a FeatureCollection, you can do so programmatically.

You can read more about how to programmatically update datasets in the [Mapbox Datasets API documentation](https://docs.mapbox.com/api/maps/#datasets).
