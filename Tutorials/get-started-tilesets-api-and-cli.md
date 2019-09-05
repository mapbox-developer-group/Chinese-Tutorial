---
title: Get started using the Tilesets API and the Tilesets CLI
description: This feature is in beta. Learn how to use the Tilesets CLI, a tool for accessing the Mapbox Tilesets API, to create new Mapbox tilesets.
thumbnail: tilesetsApiPublishedTileset
topics:
- uploads
level: 3
language:
  - Command line
prereq: Successful installation of the Tilesets CLI
prependJs:
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import WarningImage from '@mapbox/dr-ui/warning-image';"
  - "import BetaFlag from '@mapbox/dr-ui/beta-flag';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

{{<Note title='Public beta' theme="warning" imageComponent={<WarningImage color="orange" />} >}}
The Mapbox Tilesets API and the Tilesets CLI are in public beta. All features and workflows are subject to potential changes in the future.
{{</Note>}}

The Tilesets API allows you to create custom [vector tilesets](/help/glossary/tileset/#vector-tilesets) by providing source data with transformation rules called [recipes](/help/glossary/tileset-recipe). Tilesets generated using the Tilesets API can be used in any of your map styles and can be composited with any other vector tilesets.

At a high level, there are four steps required to create a new tileset using the Tilesets API:

1. [Create a tileset source](#create-a-tileset-source)
1. [Write a recipe](#write-a-recipe)
1. [Create a new tileset](#create-a-new-tileset)
1. [Publish your new tileset](#publish-your-new-tileset)

These steps can all be accomplished using the [Tilesets CLI](https://github.com/mapbox/tilesets-cli/). In this tutorial, you will use the Tilesets CLI to create a tileset source using sample data, then write a recipe that specifies how to transform that data. Then you will create a new tileset with that recipe and publish it. After it is published, you can use this tileset in a custom map style.

## Getting started

There are a few resources you'll need before getting started:

* **Create a Mapbox access token.** Create a new [access token](https://account.mapbox.com/access-tokens/) that has the scopes `tilesets:write`, `tilesets:read`, and `tilesets:list`. Do not share this token!
* **Install the [Tilesets CLI](https://github.com/mapbox/tilesets-cli/).** The Tilesets CLI is a Python tool that provides source data preparation and validation for interacting with the Tilesets API.
* **Download sample data.** This is a single line-delimited GeoJSON file.

{{
<Button href="/help/data/populated_places.geojson.ld" passthroughProps={{ download: "populated_places.geojson.ld" }} >
    <Icon name='arrow-down' inline={true} /> Download file
</Button>
}}


## Create a tileset source
{{<div className="fl mt-neg3 mr6"><BetaFlag /></div>}}

A [tileset source](/help/glossary/tileset-source) is a collection of line-delimited GeoJSON files that is saved on Mapbox.com. A tileset source is referenced by an ID, like `mapbox://tileset-source/username/hello-world`. You can think of a tileset source as a place to store your raw geographic data before turning it into a vector tileset that can be served from the Tilesets API. Tileset sources can contain multiple files. You will use a tileset source to create a new tileset "layer" later on in this tutorial.

All files used to create tileset sources must be in [line-delimited GeoJSON](https://en.wikipedia.org/wiki/JSON_streaming#Line-delimited_JSON) format. A file formatted as line-delimited GeoJSON contains one or more GeoJSON [Feature objects](https://tools.ietf.org/html/rfc7946#section-3.2) separated by newlines. Learn more about how line-delimited GeoJSON is used by the Tilesets API in the [Tileset sources troubleshooting guide](https://docs.mapbox.com/help/troubleshooting/tileset-sources/#line-delimited-geojson).

To create a tileset source, you will use the [Tilesets CLI `add-source` command](https://github.com/mapbox/tilesets-cli/#add-source). In this command, you will provide the following information:
- Your Mapbox username
- A name for the new tileset source ("hello-world" in the example command below)
- The path to the source file or files

More detail on this command and how it interacts with the Tilesets API is available in the [Tilesets CLI's documentation](https://github.com/mapbox/tilesets-cli/blob/master/README.md#add-source).

Run the following Tilesets CLI command, replacing `username` with your Mapbox account username.

```bash
$ tilesets add-source username hello-world /path/to/your/data.geojson.ld
```

This command creates a connection with the Tilesets API and uploads your source to a permanent and secure location on Mapbox’s servers.

You will see a message that tells you that the tileset source has been successfully created:

```json
{
  "file_size": 18502313,
  "files": 1,
  "id": "mapbox://tileset-source/username/hello-world",
  "source_size": 18502313
}
```

## Write a recipe
{{<div className="fl mt-neg3 mr6"><BetaFlag /></div>}}

Now that your tileset source has been created, you must provide a set of rules to tell the Tilesets API how this source's data should be transformed when you upload and publish it. These rules are referred to as "[recipes](/help/glossary/tileset-recipe)".

Recipes provide options for generating [vector tiles](/help/glossary/vector-tiles) such as degree of simplification, zoom level extent, geometry unioning, attribute manipulation, and much more. You can find more detail about all the available configuration options in the [Recipe reference](/help/troubleshooting/tileset-recipe-reference/).

Open your text editor and paste in the following basic recipe:

```json
{
  "version": 1,
  "layers": {
    "hello_world": {
      "source": "mapbox://tileset-source/username/hello-world",
      "minzoom": 0,
      "maxzoom": 5
    }
  }
}
```

Replace `username` in the `source` field with your Mapbox account username. Save the recipe to your computer as a file named `hello-world-recipe.json`.

With this recipe, you are specifying the vector tile layer name and the zoom range you want to use when the tiles are generated. This range, 0-5, is an acceptable standard default for global or country-level data. For other zoom ranges that suit your data, take a look at the zoom table in the [Recipe reference](/help/troubleshooting/tileset-recipe-reference/#zoom-level-configuration). You are also using `source` to specify that the recipe will use the tileset source that you created in the last step.

This isn’t your only chance to write your recipe. You can change it whenever you want.

## Create a new tileset
{{<div className="fl mt-neg3 mr6"><BetaFlag /></div>}}

Now you will create a new tileset using your recipe using the [Tilesets CLI `create` command](https://github.com/mapbox/tilesets-cli/#create).

You will give your new tileset a tileset ID. This will be the main resource you reference when adding the tileset to your map styles in the future. The tileset ID is a combination of your Mapbox username plus an identifier that is 32 characters or less. The identifier cannot include spaces, but it can include `-` and `_` special characters. In the example below, the tileset ID is `username.hello-world-tiles`. When you run the command, replace `username` with your Mapbox account username.

Use the `--recipe` flag to reference the recipe you created in the last step. This gives the Tilesets API a set of rules to follow as it generates the tileset.

Use the `--name` flag to create a human-readable name for your tileset. The name is limited to 64 characters. If you do not provide a name, one will be randomly generated.

To create the tileset, run the following Tilesets CLI command:

```bash
$ tilesets create username.hello-world-tiles --recipe hello-world-recipe.json --name "hello world"
```

You should see a successful response message:

```bash
message: 'Successfully created username.hello-world-tiles.'
```

If you are signed into Mapbox Studio, you will see this new tileset on the [tilesets page](https://studio.mapbox.com/tilesets/). Since it has not been published, it will appear as "empty".

{{
<AppropriateImage imageId="tilesetsApiNewTileset" alt="Screenshot showing Mapbox Studio tilesets page with an empty tileset" />
}}

Now that you have successfully created a tileset, you can publish it!

## Publish your new tileset
{{<div className="fl mt-neg3 mr6"><BetaFlag /></div>}}

Publishing your tileset is an active step that tells the Mapbox Tilesets API to take the following steps:

1. Read your tileset’s recipe.
2. Retrieve the tileset source data you created.
3. Create vector tiles from the data in the tileset source by applying the transformation rules outlined in the recipe.

To publish your tileset, you will use the [Tilesets CLI `publish` command](https://github.com/mapbox/tilesets-cli/#publish). Run the following command, replacing `username` with your Mapbox account username.

```bash
$ tilesets publish username.hello-world-tiles
```

You’ll see a success message, which means that your publish request has been queued and the Tilesets API has begun generating your tileset!

```json
{
  "jobId": "<job_id>",
  "message": "Processing username.hello-world-tiles."
}
```

The time it takes to generate your final tileset is determined by the size of your source data and the complexity of your recipe. For example, if you've specified a larger range of zoom levels, this will generate more vector tiles.

You can check the status of your tileset at any time with the [Tilesets CLI `status` command](https://github.com/mapbox/tilesets-cli/#status):

```bash
$ tilesets status username.hello-world-tiles
```

This shows how many jobs have completed, errored, are processing, and have been queued. Your job should only take a few minutes to show `"success": 1` once processing finishes.

```json
{
      "id": "username.hello-world-tiles",
      "last_completed_job": "<job_id>",
      "queued": 0,
      "processing": 0,
      "success": 1
}
```

Once publishing has completed successfully, you will see the new tileset in your [tilesets page](https://studio.mapbox.com/tilesets/). This tileset is now ready to be used in your custom map styles!

{{
<AppropriateImage imageId="tilesetsApiPublishedTileset" alt="Screenshot showing Mapbox Studio tilesets page with the newly published tileset" />
}}

Need to make changes to your source data or your recipe? You can repeat the process above as many times as you like. For instance, to increase the zoom level to 10 and include an additional line-delimited GeoJSON file, you can repeat steps three and four of this tutorial until you're satisfied with the output tileset.

## Additional resources

- **Add a tileset to a style.** Not sure how to add your new tileset to your style? You can find detailed steps for this in our [Make a choropleth map tutorial](/help/tutorials/choropleth-studio-gl-pt-1/#add-a-new-layer).
- **Recipe examples.** Recipes are the primary way to manipulate the look of your tileset. If you aren’t sure what recipe to use, we recommend reading through the [Recipe examples](/help/troubleshooting/tileset-recipe-examples) page, which has samples of common and complex use cases, plus descriptions for every part of the recipe.
- **Recipe reference.** The [Recipe reference](/help/troubleshooting/tileset-recipe-reference) documents all the available options for creating recipes and includes mini examples.
- **Tilesets API documentation.** The Mapbox Tilesets CLI is a tool for accessing the Tilesets API. The [Tilesets API documentation](https://docs.mapbox.com/api/maps/#tilesets) has information about all the Tilesets API's endpoints and options.  
- **Tilesets CLI documentation.** The [Tilesets CLI](https://github.com/mapbox/tilesets-cli/) has more commands than those discussed in this tutorial. The [documentation](https://github.com/mapbox/tilesets-cli/blob/master/README.md) in the GitHub repository outlines all the available commands, such as viewing or updating a recipe, validating source data, or converting data into line-delimited GeoJSON.
