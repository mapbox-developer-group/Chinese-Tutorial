---
title: Point-in-polygon query with Mapbox Boundaries
description: Query data in v2 of the Mapbox Boundaries tileset.
level: 2
topics:
- data
language:
- JavaScript
thumbnail: pointInPolygonQueryWithEnterpriseBoundaries
prereq: Familiarity with front-end development and access to Mapbox Boundaries.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
<Note
  title="Access to Mapbox Boundaries"
  imageComponent={<BookImage />}
>
  <p>Access to the Mapbox Boundaries tilesets are controlled by Mapbox account access token. If you do not have access on your account, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access to Boundaries tilesets.</p>
</Note>
}}

Mapbox Enterprise users can add global administrative, postal, and statistical boundaries to their maps and data visualizations. This guide covers how to use Mapbox Boundaries with the Mapbox Tilequery API to query points in polygons.

## Getting started

Mapbox Boundaries are available as a part of an Enterprise plan. If you do not have an Enterprise plan or if you do have an Enterprise plan and would like to add access to Mapbox Boundaries, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access. Access to the Boundaries tilesets are controlled by your Mapbox account access token.

## About the Tilequery API

The [Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) allows you to get data from a tileset without necessarily  rendering a map. You can use the Tilequery API to match points to polygons, in other words, you can provide the coordinates for a point and determine which (if any) polygons in a specified tileset exist at that point.

Here's what a Tilequery API request using a Boundaries tileset would look like:

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a0-v2/tilequery/{longitude,latitude}.json?access_token={{ <UserAccessToken /> }}
```

{{
  <Note imageComponent={<BookImage />}>
    <p>Be sure to use an access token from an account that has access to Mapbox Boundaries.</p>
  </Note>
}}

If the specified point is within a polygon, the Tilequery API response will include a GeoJSON-format body with all features in the tileset. The `id` property value of the first feature returned is the ID of the Boundaries feature that contains the queried point.

Since the feature lookup table contains all Mapbox Boundaries parent features, only one API request is required per point to find all matching parent boundaries. For example, you can query the admin-2 boundary of a point in Italy, and use the lookup table to find the parent features at admin-1 and admin-0.

## Query Mapbox Boundaries

Below is an example API response from a sample query to admin-2 in Italy. The query URL is:

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a2-v2/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

{{
  <Note imageComponent={<BookImage />}>
    <p>Be sure to use an access token from an account that has access to Mapbox Boundaries.</p>
  </Note>
}}

The `id` returned is the identifier of the Boundaries feature containing the point at admin-2.

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          12.87,
          43.1
        ]
      },
      "properties": {
        "id": "ITA2054",
        "worldview": "all",
        "tilequery": {
          "distance": 0,
          "geometry": "polygon",
          "layer": "boundaries_admin_2"
          }
      }
    }
  ]
}
```

### Query multiple tilesets

You can query multiple admin levels in one API call using tile compositing. The query below will return the `id`s at a location for admin-1, admin-2, and admin-3:

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a3-v2,mapbox.enterprise-boundaries-a2-v2,mapbox.enterprise-boundaries-a1-v2/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

{{
<Note
  imageComponent={<BookImage />}
>
  <p>Find the complete list of Boundaries tilesets in the <a href="https://www.mapbox.com/vector-tiles/enterprise-boundaries-v2">reference documentation</a>.</p>
</Note>
}}

This technique allows for aggregating and visualizing points at any admin level or multiple admin levels, down to individual points, as an API service.

## Next steps

### Learn more about the Tilequery API

Build an application that determines which timezone you are in using the Mapbox Tilequery API and the native HTML geolocation API with our [Create a timezone finder](/help/tutorials/create-a-timezone-finder-with-mapbox-tilequery-api/) tutorial.

### Learn more about Mapbox Boundaries

Learn more about how you can use Mapbox Boundaries.

- [Data-joins with Mapbox Boundaries](/help/tutorials/data-joins-with-enterprise-boundaries/): The data-join technique involves inner joins between local data, such as the unemployment rate by US state, to vector tile features, such as admin boundaries in Mapbox Boundaries, using data-driven style notation.
- [Extend Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/): You can extend Mapbox Boundaries with any custom data you need for your application. This could mean adding school district, city, market, or property boundaries to your application &mdash; all with the same performance and API features of the native product.

### Advanced use cases

You can also explore this [end to end example](https://www.mapbox.com/labs-sandbox-demos/vt_polygons/), which uses the concepts outlined in both this point-in-polygon query tutorial and the [data-join](/help/tutorials/data-joins-with-enterprise-boundaries/) tutorial to create an application featuring an interactive choropleth map.

![an end to end example using the data-join technique and Tilequery API](/help/img/data/enterprise-boundaries-choropleth-demo.gif)
