---
title: Add OpenStreetMap data to your Mapbox project
description: Learn how to export OpenStreetMap data to be used in your Mapbox project.
thumbnail: overpassTurbo
level: 2
topics:
- data
- uploads
language:
- No code
prereq: Learn to navigate the OpenStreetMap tagging system.
contentType: tutorial
---

If you're looking to use [OpenStreetMap](https://www.osm.org) data in Mapbox Studio, look no further! In this guide you'll learn how to use [Overpass Turbo](https://overpass-turbo.eu/) to query OpenStreetMap data and extract specific features in a given area. You'll be exporting ski lifts and trails at [Mt. Bachelor](https://en.wikipedia.org/wiki/Mount_Bachelor), a popular ski resort in central Oregon. If you'd like to extract OpenStreetMap features programmatically rather than with a user interface, read the [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) documentation for more information.

## Getting started

If this is your first time working with OpenStreetMap we recommend reading about OpenStreetMap and Mapbox in the [Our map data](/help/how-mapbox-works/mapbox-data/) guide before you get started.

### OpenStreetMap features

In OpenStreetMap, contributors can tag physical features like buildings or roads to help describe them. For example, to add a `building` tag to a feature, the key for the feature would be `building` and the value would be `yes`.

![example of adding a building tag in OpenStreetMap](/help/img/3rdparty/overpass-tag.jpg)

If we want to be more specific about what type of building it is, for example a hotel, we can change the tag to `building=hotel`. Now others who access the data will know that the feature is a building _and_ that it's a hotel. This is especially helpful for someone who is trying to query all hotels in a particular area.

You can find the list of all keys and values on the [OpenStreetMap Features wiki](http://wiki.openstreetmap.org/wiki/Map_Features).

### OpenStreetMap data and Mapbox Streets

[Mapbox Streets](https://www.mapbox.com/developers/vector-tiles/mapbox-streets-v7/) uses OpenStreetMap as its main data source. Mapbox Streets is a vector [tileset](/help/glossary/tileset) that is available to all Mapbox users and is used in almost all Mapbox template styles. If you create a new style based on a Mapbox template in the Mapbox Studio style editor, odds are the style includes the Mapbox Streets tileset.

If you want to use OpenStreetMap data in Mapbox Studio, the quickest way is to use Mapbox Streets as a source in your style. Mapbox Streets is a curated tileset created from OpenStreetMap data, and it is updated continuously as OpenStreetMap is edited. To see which OpenStreetMap features are included in your version of Mapbox Streets, visit the [Mapbox Streets documentation](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/). If you want to add features to your map that are not included in Mapbox Streets, you'll need to use other tools such as Overpass Turbo to extract OpenStreetMap data.

## Use the OpenStreetMap Wiki

In this exercise, you need to find some of the features at the Mt. Bachelor Ski Resort:

- Downhill ski trails
- Chair lifts
- Lift stations

First, you need to find the proper tags for these features. You can do this by opening OpenStreetMap and clicking a feature to find its tags or by searching the [OpenStreetMap Map Features wiki](http://wiki.openstreetmap.org/wiki/Map_Features). Search the [wiki](http://wiki.openstreetmap.org/wiki/Map_Features) to find the keys and values that most closely resemble the features you want to query.

From the wiki, you can find the following key and values for our features:

| **Key**  | **Value**  | **Element**  | **Comment**  |
|---|---|---|---|
| piste:type| downhill |Area/Way| An alpine/downhill ski route. Ways should be used for trails connecting the routes. This automatically implies `oneway=yes`. The direction of the way should be the downhill direction.	|
| aerialway | chair_lift | Way | Looped cable with a series of single chairs or benches, exposed to the open air. Implies `oneway=yes`; where passengers can be carried in the reverse direction, tag with `oneway=no`.|
| aerialway| station	| Node Area| A station, where passengers can enter and/or leave the aerialway|


Now that you have the correct keys and values, open [Overpass Turbo](http://overpass-turbo.eu/) to query OpenStreetMap for the data.

## Use Overpass Turbo

Start by taking a quick tour of Overpass Turbo's interface.

![screenshot of the Overpass Turbo interface](/help/img/3rdparty/overpass-portland.png)

### Navigate the interface menu

- **Run.** Runs the current query in the code window. The result is highlighted on the map to the right.
- **Share.** Links to the current query.
- **Export.** Exports the queried data into different formats for use in other applications.
- **Wizard.** A query wizard that allows you to find features based on their keys and values.
- **Save.** Saves your query for future use.
- **Load.** Load a sample query or your saved query.
- **Settings.** Allows you to change the map background, language, and other features of the interface.
- **Help.** Useful hints and topics about the interface.

__Tabs__

- **Map.** The default map view (you can swap background with other web services).
- **Data.** A raw data view.

### Run a query

When you first launch [Overpass Turbo](http://overpass-turbo.eu/), it starts you off with an example for querying [drinking fountains](http://overpass-turbo.eu/s/3Xp). Overpass Turbo uses a simplified version of the XQuery to query OpenStreetMap features.

You must click **Run** for Overpass to show the results on the map. Once you've executed the query, Overpass will highlight the features that meet the query conditions.

![Portland drinking fountains](/help/img/3rdparty/overpass-portland-df.png)

Take a closer look at the structure of the query:

```
/*
This is an example Overpass query.
Try it out by pressing the Run button above!
You can find more examples with the Load tool.
*/
node
  [amenity=drinking_water]
  (\{\{bbox\}\});
out;
```

The query starts by looking for features with the type `node`. Then it checks the key `amenity` against the value `drinking_water`. A bounding box (southwest and northeast coordinate pairs) can be issued, or in this case, a `bbox` variable will grab the current window's extent.

Now that you're familiar with Overpass Turbo's interface, you can use it to grab the ski features.

### Find the ski amenities

Start by using the search tool to locate `mt. bachelor, oregon`. The search tool is located on the map to the right of the zoom buttons.

Once you've located and zoomed to Mt. Bachelor, click the **Wizard** button from the toolbar and paste the following statement in the Query Wizard window:

```sql
aerialway=station OR aerialway=chair_lift OR piste:type=downhill
```

These are the keys and values we found from the OpenStreetMap Features wiki. Click **Run**. You should see that Overpass has highlighted the features on the map.

![screenshot of OverpassTurbo querying ski features](/help/img/3rdparty/overpass-build-query.png)

### Export data

Now that Overpass has found the features, export them. Click the **Export** button in the toolbar, select **GeoJSON**.

![screenshot of the export options in Overpass Turbo](/help/img/3rdparty/overpass-export.png)

You can also share queries in Overpass from the **Share** button in the toolbar. [Here's the saved query we made](http://overpass-turbo.eu/s/f5F).

## Finished Product

You've learned how to query and export data from OpenStreetMap using Overpass Turbo! Now that you have your data, you can start building with Mapbox by [uploading your data](https://www.mapbox.com/studio-manual/overview/geospatial-data/) as a [dataset](https://www.mapbox.com/studio-manual/reference/datasets/) or [tileset](https://www.mapbox.com/studio-manual/reference/tilesets/) in [Mapbox Studio](https://www.mapbox.com/studio), and creating a new custom style using the Mapbox Studio style editor. Read the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/) to get started.
