---
title: Create a map in Unity
description: Use the Mapbox Maps SDK for Unity to create a visualization of 3D buildings on top of a 3D terrain map for use in a Unity application.
thumbnail: createAMapInUnity
level: 1
topics:
- unity
language:
- No code
prereq: Familiarity with Unity.
contentType: tutorial
---

This tutorial will walk you through how to create a visualization of 3D buildings on top of a 3D terrain map for use in a Unity application. You will:

- Set up a Mapbox project in Unity.
- Learn about the Mapbox-specific terminology, tools, and services you’ll use to build your visualization.
- Add a map to your scene.
- Customize your map for your specific needs.
- Learn how to add buildings and other vector data.

This tutorial is for versions 1.4.0 and beyond. If you are using version 1.3.0 or earlier, read the [mesh generation tutorials](/help/tutorials/unity-mesh-pt-1/) instead.

## Getting started

Before getting started, you’ll need to:

1. **Install the Mapbox Maps SDK for Unity**. For full installation instructions, visit [https://www.mapbox.com/unity-sdk](https://www.mapbox.com/unity-sdk).
2. **Create an empty Unity project**.
3. **Configure your Mapbox access token in your Unity project**. For token configuration instructions, visit [http://www.mapbox.com/unity-sdk/#token](http://www.mapbox.com/unity-sdk/#token).

## Set up your project

Your new, empty scene will need a Map object to display a map. We provide a Map prefab already that you can drag and drop into your scene.

![where to find the Map prefab](/help/img/unity/create-a-map-getting-started-unity-1.png)

This Map object comes with an `Abstract Map` script, where you can adjust map settings like location, map style, elevation, and more.

To see what the default Map looks like, hit **Play**.

![default map in Unity](/help/img/unity/create-a-map-getting-started-unity-2.png)

You have a map! Note that you may need to change the camera’s position to see the map properly in the Game panel, but you can see it in the Scene panel.

## Customize your map

Now you’ll learn how to style two kinds of maps: one with rich satellite imagery and elevation data, and one with vector data to show buildings. You will learn how to use various settings in `Abstract Map` to change a map’s location, map style, elevation, and vector layers.

### Create a map of Mt. Hood, Oregon

Select your Map object and look at the Inspector window. Under the `Abstract Map` general settings, either change the location to `45.374218, -121.688341`  or search “Mt Hood”. Set the zoom level to `13`. Open the “Others” settings and toggle `Snap Map to Zero`.

![map settings for Mt Hood](/help/img/unity/create-a-map-getting-started-unity-3.png)

Now open the image settings and change the `Data Source` to “Mapbox Satellite”. Finally, open the terrain settings and change the `Elevation Layer Type` to “Terrain with Elevation”.

![map settings for Mt Hood](/help/img/unity/create-a-map-getting-started-unity-4.png)

Save your scene and hit play. Switch to your Scene panel and you’ll see something like this:

![map of Mt Hood](/help/img/unity/create-a-map-getting-started-unity-5.png)

Now you'll make a map of downtown Manhattan!

### Create a map of downtown Manhattan

To make this map of Manhattan, you can either start over in a new scene, or change the settings in your existing scene. It’s up to you!

First set the location to `40.706843, -74.011370` or search “New York Stock Exchange”, and set the zoom level to 17. Next, go to the image settings and change the `Data Source` to “Mapbox Dark”. In the terrain settings, change the `Elevation Layer Type` to “Flat Terrain”.

![map settings for Manhattan](/help/img/unity/create-a-map-getting-started-unity-6.png)

Now open up the vector settings. Change the `Data Source` to “Mapbox Streets”. Create a new visualizer by clicking the “Add Visualizer” button. It will now show up in the vector layer visualizers list as “Untitled”. Click it and hit the `Enter` key to rename it to “Buildings”.

![vector settings for Manhattan](/help/img/unity/create-a-map-getting-started-unity-7.png)

Click your “Buildings” visualizer and find the `Extrusion Type` setting. Change it to “Property Height”. Next, look for the `Material Options` setting. Next to `Roof Material` and `Wall Material` is a small circular icon. Click it, and select ”BuildingMaterial” for both.

![building settings for Manhattan](/help/img/unity/create-a-map-getting-started-unity-8.png)

Hit play to see Manhattan with buildings!

![map of Manhattan](/help/img/unity/create-a-map-getting-started-unity-10.png)

### Next steps

To learn more about what you can do with Mapbox Maps SDK for Unity, read the [SDK documentation](https://www.mapbox.com/unity-sdk/overview/).
