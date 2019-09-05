---
title: Unity applications
description: Learn how the Mapbox Maps SDK for Unity works, how to use it, and how to get started building applications.
image: /img/narrative/game-develop.svg
topics:
  - unity
contentType: guide
---

The [Mapbox Maps SDK for Unity](https://www.mapbox.com/unity-sdk/) is a set of tools to build [Unity](https://unity3d.com/) applications from real map data. It consists of a robust API for interfacing with [Mapbox web services](https://docs.mapbox.com/api/) and converting map resources into game objects as well as a robust graphical user interface built on top of the Unity platform. This guide provides an overview of how the [Mapbox Maps SDK for Unity](/help/glossary/mapbox-maps-sdk-for-unity/) works, how to use it, and how to get started building applications.

<img src="/help/img/unity/unity-blocks.png" alt="unity screenshot of sample project">

## How the Mapbox Maps SDK for Unity works

The [Mapbox Maps SDK for Unity](https://www.mapbox.com/unity-sdk/) is designed to help Unity developers add dynamic map data to their games and applications by providing a straightforward programmatic and graphical interface to Mapbox's web services APIs, including:
- [Vector Tiles API](https://docs.mapbox.com/api/maps/#vector-tiles)
- [Raster Tiles API](https://docs.mapbox.com/api/maps/#raster-tiles)
- [Static Images API](https://docs.mapbox.com/api/maps/#static-images)
- [Geocoding API](https://docs.mapbox.com/api/search/#geocoding)
- [Directions API](https://docs.mapbox.com/api/navigation/#directions)
- [Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching)

### Dynamic data

While some map-focused Unity plugins are designed to help developers build static game environments from map data, the Mapbox Maps SDK for Unity is designed to request and render map data at runtime. This means that applications built with the Maps SDK for Unity will always display the most recent version of spatial data. It also means that games and applications only ever request the subset of data that corresponds with the area the user is viewing, keeping games and applications lightweight.

### Mesh generation

The Mapbox Maps SDK for Unity provides the ability to generate meshes to create 2D or 3D maps, with satellite imagery, custom map styles, terrain data, and points of interest. See the [mesh generation tutorial](/help/tutorials/unity-mesh-pt-1/) to get started.

### AR support

The Mapbox Maps SDK for Unity provides support for augmented reality, whether you're making a tabletop AR app or the next PokemonGo.

## Using the Mapbox Maps SDK for Unity

The Mapbox Maps SDK for Unity is used with the [Unity](https://unity3d.com/) desktop application.

### Installing the Mapbox Maps SDK for Unity

The Mapbox Maps SDK for Unity is available [via direct download](https://www.mapbox.com/unity/). See the Mapbox Maps SDK for Unity documentation for complete [installation instructions](https://www.mapbox.com/unity-sdk/#install).

### Creating game objects

The Mapbox Maps SDK for Unity can be used to build rich environments from a variety of different types of data, including terrain data, raster map tiles, and vector map tiles, among others.

#### Terrain

The Mapbox [terrain-rgb](https://www.mapbox.com/blog/terrain-rgb/) tileset is designed for high resolution elevation visualizations and it is especially well-suited to creating 3D meshes with Unity. See the [Mesh generation basics](https://www.mapbox.com/mapbox-unity-sdk/docs/03-examples.html#mesh-generation-basics) example for more information.

<img src="/help/img/unity/unity-terrain.png" alt="unity screenshot of terrain">

#### Features from vector tiles

Whether you're using a [Mapbox tileset](https://www.mapbox.com/vector-tiles/) or a custom tileset you created via the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads), the Mapbox Maps SDK for Unity can request vector tiles, convert them into game objects or meshes, and render them alongside the rest of your game data. See the [Slippy map](https://www.mapbox.com/mapbox-unity-sdk/docs/03-examples.html#slippy-vector-terrain) example for more information.

<img src="/help/img/unity/unity-city.png" alt="unity screenshot of city">

### Accessing Mapbox web services

The Mapbox Maps SDK for Unity can connect your game or application to many of Mapbox's web services APIs, including the Mapbox [Vector Tiles API](https://docs.mapbox.com/api/maps/#vector-tiles) [Raster Tiles API](https://docs.mapbox.com/api/maps/#raster-tiles), [Static Images API](https://docs.mapbox.com/api/maps/#static-images), [Geocoding API](https://docs.mapbox.com/api/search/#geocoding), [Directions API](https://docs.mapbox.com/api/navigation/#directions), and [Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching). See the various [Playground](https://www.mapbox.com/mapbox-unity-sdk/docs/03-examples.html#playground) examples for more information on interacting with Mapbox APIs.

### Publishing

The Mapbox Maps SDK for Unity works anywhere Unity works, including, desktop, and mobile and coming soon to the web.

### Pricing

Mobile applications built with our Maps SDK for Unity track usage with [monthly active users](/help/glossary/monthly-active-users/) (MAU). This means each device using your app within a month counts as a single MAU. All other apps built with Unity are charged by tile requests. All types of applications are metered for usage of the Mapbox APIs, like Geocoding and Directions, when they surpass what’s included with the free plan.
