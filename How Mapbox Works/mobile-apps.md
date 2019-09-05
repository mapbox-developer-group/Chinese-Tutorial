---
title: Mobile applications
description: Learn how the Mapbox mobile SDKs work and how to add Mapbox maps to a mobile application.
image: /img/narrative/mobile-develop.svg
topics:
  - mobile apps
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: guide
---

The [Mapbox Maps SDK for iOS](https://docs.mapbox.com/ios/maps/overview) and the [Mapbox Maps SDK for Android](https://docs.mapbox.com/android/maps/overview) are open-source tools for adding Mapbox maps to mobile applications. These SDKs leverage Mapbox's open source OpenGL-based renderer, [Mapbox GL Native](https://github.com/mapbox/mapbox-gl-native), and support a full suite of dynamic styling features and interactivity. You can add your custom Mapbox style, search for locations using the Mapbox Geocoding API, or get directions, all without leaving your app. Where possible, the Mapbox Maps SDKs for iOS and Android provide straightforward drop-in replacements for common platform-specific maps SDKs.

This guide outlines how the Mapbox mobile SDKs work and how Mapbox services can be added to a mobile application.

<img src="/help/img/mobile/mobile-dds.jpg" alt="unity screenshot">

## How the Mapbox mobile SDKs work

The Mapbox Maps SDKs for [iOS](https://docs.mapbox.com/ios/maps/overview/) and [Android](https://docs.mapbox.com/android/maps/overview/) allow you to add interactive maps to your mobile applications, define custom and dynamic style rules, manipulate custom data, and interface with Mapbox web APIs.

### Client-side rendering

At the heart of the Mapbox mobile SDKs is Mapbox GL: a powerful rendering engine that reads **raw data** and **style rules** and outputs complete, rendered maps on the device. While traditional server-side rendering works for creating static map tiles, the resulting tiles cannot be styled once they reach the client. With Mapbox GL, tiles can be rendered directly on the client. This enables you to create dynamic visualizations, add and remove layers dynamically, and adjust your style's properties based on data or the user's unique needs.

### Layers and runtime styling

Many popular map libraries conform to the "basemap-overlay" paradigm in which a map is composed of two distinct types of layers: the basemap (a complete map that provides the foundation and context for the map) and the overlay (often interactive data that is added _on top of_ the basemap, usually at runtime).

#### Layers

While the basemap-overlay strategy has worked well for a long time, there are many drawbacks. Overlays often obscure basemap labels below and large overlay datasets quickly become cumbersome.

Mapbox maps do away with the basemap-overlay strategy and treat _everything_ on the map as a layer that you can style independently and move up and down the rendering stack. In this approach to displaying maps, a layer is a **styled representation of vector or raster data** that is rendered using rules about how Mapbox should draw certain data on the map. This strategy allows data to be added without obscuring contextual features like labels.

#### Runtime styling

Because everything in the map is rendered from vector or raster tiles on the device in real time, Mapbox maps have no distinction between baselayers and overlay layers. This means that _every element of the map_ can be added, removed, and styled dynamically at [runtime](/help/glossary/runtime-styling/), like overlays in other mapping libraries.

#### Data-driven styling

[Data-driven styling](/help/glossary/data-driven-styling/) enables you to change a map style based on data properties. For example, you can change the radius of a circle at an intersection based on the number of pedestrians crossing the intersection, or change the color of a state boundary fill-layer based on the population of each state.

<div class='align-center'><img alt='graduated circle map using data-driven styling' src='/help/img/screenshots/dds-pedestrian_foot_traffic_at_intersections.png'></div>

### Feature querying and interactivity

One benefit of rendering maps on the device at runtime is that it enables the map user to query _any feature_ in the map, including what would have once been considered the "basemap." Using [feature querying](/help/glossary/feature-querying/), you can add interactivity to any layer in your map style. For example, you can use feature querying to build an app that allows your users to tap on a park polygon to open a popup that contains information about the park.

The Mapbox mobile SDKs include methods for querying features that have been rendered on the map or features that have not been rendered, but are present in the tiles loaded in the map view. Explore the [Select a feature using feature querying](https://docs.mapbox.com/ios/maps/examples/select-layer/) example to see feature querying in action.

<div class='align-center'><img alt='selecting individual states with feature querying' src='/help/img/mobile/mobile-select-layer.gif'></div>

### The camera

The camera is the map’s field of view. The viewpoint of the camera in many popular mapping libraries is determined by the map’s centerpoint and zoom level. The mobile SDKs also include parameters for adjusting the map’s perspective.

- **Centerpoint**: in decimal degrees and longitude, latitude order.
- **Zoom level**: any number between 0 and 22. This can be a fractional number like 1.5 or 6.2.
- **Bearing**: a map rotation value in degrees. The map will be rotated and details like text labels will react by rotating right-side-up.
- **Tilt**: also in degrees, a value by which the map will be tilted in perspective.

### Offline maps

Applications built with our mobile SDKs can download maps of selected regions for use when the device lacks network connectivity. Offline maps are useful for apps whose users expect to travel through areas with limited data connectivity or who want to save on cellular roaming charges while traveling abroad.

To estimate the number of tiles needed to download a region offline, use our offline tile count estimator. Please note that this only generates an _estimate_ of the number of tiles needed to load a defined region offline. The _size_ of the download will vary according to the location being downloaded and the style being used in your application.

<a class="txt-ms txt-bold link" href="/help/interactive-tools/offline-estimator/">Offline tile count estimator{{<Icon name='arrow-right' inline={true} />}}</a>

Our mobile SDKs also automatically cache tiles and other resources that are requested during normal use of the app. These resources are stored in the same database as offline resources, but unlike offline resources, they are limited to 50 MB of space. When this limit is reached, the least-recently used resources that aren't shared by an [offline region](/help/glossary/offline-region/) will be evicted to make room for newer resources.

Learn more about how to use offline maps for [iOS](https://docs.mapbox.com/ios/api/maps/{{constants.VERSION_IOS_MAPS}}/Classes/MGLOfflineStorage.html) and [Android](https://docs.mapbox.com/android/maps/overview/offline/) in the respective documentation. For more background on offline maps, read our [Offline maps](/help/troubleshooting/mobile-offline) troubleshooting guide.

### Telemetry

By default, whenever your application causes the user's location to be gathered it sends anonymized location and usage data to Mapbox. But your users should be in charge of their own location data and when it is shared.

If you're developing a native app with one of the Mapbox mobile SDKs, our terms of service require that you provide a [telemetry](https://www.mapbox.com/telemetry/) opt-out option within your app for all end users. The default attribution control includes an opt out button. If you hide the [attribution control](/help/how-mapbox-works/attribution/), you must provide an alternative opt out method your users can use. You are responsible for allowing your users to opt out of Mapbox Telemetry.

## Adding Mapbox to your mobile app

Mapbox provides a variety of tools to help you integrate Mapbox maps and our other web services, like directions, geocoding, and static maps, into your mobile application.

### Maps

To get started, visit the mobile SDK overview pages, which include installation instructions, API documentation, and sample code:

- [Mapbox Maps SDK for Android](https://docs.mapbox.com/android/maps/overview/)
- [Mapbox Maps SDK for iOS](https://docs.mapbox.com/ios/maps/overview/)

If you would like a more guided introduction to building your first mobile app with one of our Maps SDKs, explore our first steps guides:

- [First steps with the Mapbox Maps SDK for iOS](/help/tutorials/first-steps-ios-sdk/)
- [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/)

### Mapbox web services

To keep the Mapbox Maps SDKs for iOS and Android small, we provide separate libraries for interfacing with Mapbox web services like the [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions), [Geocoding API](https://docs.mapbox.com/api/search/#geocoding), and [Static Images API](https://docs.mapbox.com/api/maps/#static-images).

On Android, the **Mapbox Java SDK** provides convenient interfaces to many Mapbox web services APIs as well as a handful of useful utilities for performing common geospatial tasks.

On iOS, **MapboxGeocoder.swift**, **MapboxDirections.swift**, and **MapboxStatic.swift** provide interfaces to the Mapbox Geocoding API, Directions API, and Static Images API.

For installation instructions, API documentation, and code examples, please visit each platform's respective documentation pages:

- [Mapbox Java SDK](https://docs.mapbox.com/android/java/)
- [Mapbox API libraries for iOS](https://docs.mapbox.com/ios/maps/overview/#integration-with-other-tools)

### Mapbox Navigation SDKs

Built on top of the [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions), the [Mapbox Navigation SDKs](/help/glossary/mapbox-navigation-sdk/) provide all the logic necessary to implement a navigation experience in your app. The Mapbox Navigation SDKs include critical features like:

- Drop-in turn-by-turn navigation UI.
- Automotive, cycling, and walking directions.
- Traffic avoidance.
- Maneuver announcements.
- Text instructions.
- Text to speech support.
- Automatic rerouting.
- Snap to route.

To include the Mapbox Navigation SDKs in your application, please visit the respective documentation pages for installation instructions, API reference, and sample code:

- [Mapbox Navigation SDK for iOS](https://docs.mapbox.com/ios/navigation/overview/)
- [Mapbox Navigation SDK for Android](https://docs.mapbox.com/android/navigation/overview/)

### Hybrid frameworks
Third parties have created plugins and integrations that allow to you use Mapbox SDKs with a variety of alternative development platforms.

See our [hybrid pricing guide](/help/account/pricing/#hybrid-applications) for more information on how usage of your app will be billed.

#### Hybrid frameworks using Mapbox JavaScript APIs

Creating hybrid apps with [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js) or [Mapbox.js](https://docs.mapbox.com/mapbox.js) is also possible.

#### Potential problems

Contact the maintainers of these integrations directly if you have issues or implementation questions, as we are not able to provide official support for hybrid frameworks.

Development of the Mapbox Maps SDKs for [iOS](https://docs.mapbox.com/ios/maps/overview/) and [Android](https://docs.mapbox.com/android/maps/overview/) move quickly, and new features are released on a regular basis. Third-party plugins that rely on these native SDKs may break with new versions, lag behind the official releases, and not support all available features.

<!--copyeditor disable best-->

Our native SDKs work best when you use them directly. Get started now with our first steps guides for [Android](/help/tutorials/first-steps-android-sdk) and [iOS](/help/tutorials/first-steps-ios-sdk).
