---
title: Map design
description: Learn how Mapbox styles work and where you can go to learn more and get started designing your map.
image: /img/narrative/design.svg
topics:
  - map design
prependJs:
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: guide
---

You can use Mapbox to control nearly every aspect of the map design process, including uploading custom data, tweaking your map's color scheme, adding your font, creating data-driven visualizations, and more. The core of the map design process is the **style**: a document, written in JSON, that defines exactly how your map should be drawn. Because all Mapbox styles conform to the open source [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec/), your maps can be rendered consistently across multiple platforms, including on the web with Mapbox GL JS, the Mapbox Static Images API, on mobile with the Mapbox Maps SDKs for Android and iOS, and with any third party libraries that are designed to read Mapbox styles. This guide explains how Mapbox styles work and where you can go to learn more and get started designing your map.

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-styles-work.html" />
}}

Style documents, or Style JSON, contain style rules that are used by a renderer to display the map you see in your browser or device. In this example, you can see references to the style's data and images and instructions on how to render them in the **Style JSON** on the left and the **rendered live map** on the right. The map is displayed in your browser after Mapbox GL draws the final map using the style JSON and the tilesets it refers to.

## How map styles work

You must write style JSON according to a strict specification for the renderer to interpret it and display the map in your browser.

### Mapbox Style Specification

The [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-style-spec/) defines the information that should be included in a style document for the renderer to display the map, including the title, values for the initial [camera](/help/glossary/camera/) position, sources and other resources used in the style, and the styling rules for the map's layers. The complete requirements are listed in the Mapbox Style Specification, but some of the key concepts to understand are:

The map that you see in your browser or on your device is the result of applying **style rules** (Style JSON) to **data sources** (usually map tiles or GeoJSON) to render a complete map. In the language of the Mapbox Style Specification, data sources are called **sources** and the style rules you apply to that data are organized into **layers**. You cannot create a map without specifying both sources and layers.

- [**Sources**](https://www.mapbox.com/mapbox-gl-js/style-spec/#sources). Sources tell the renderer what kind of data you would like to include and where to find it.
- [**Layers**](https://www.mapbox.com/mapbox-gl-js/style-spec/#layers). A layer is a styled representation of the data in a source. It includes information about how the layer should appear on the map, including color, opacity, font, and more.

If you are using any icons, images, or fonts in your map, your style will need to include a `sprite` or `glyphs` property.

- [**Sprite**](https://www.mapbox.com/mapbox-gl-js/style-spec/#sprite). Any icons or images in your style will need to be stored in a sprite. Read more about [how sprites work](/help/glossary/sprite).
- [**Glyphs**](https://www.mapbox.com/mapbox-gl-js/style-spec/#glyphs). Glyphs are used to display the fonts you are using in your style. A style's glyphs property provides a URL template for loading signed-distance-field glyph sets in `PBF` format.

### Using styles

Map styles work with [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/), the Mapbox Maps SDKs for [Android](https://docs.mapbox.com/android/maps/overview/) and [iOS](https://docs.mapbox.com/ios/maps/overview/), and any third party software designed to read Mapbox styles. Style rules and tilesets are combined and rendered completely on the computer or mobile device that has requested them. Because styles are designed to work with GL-based renderers, you can alter your style programmatically after the map has been loaded.

### Data-driven styles

Data-driven styles allow you to change a layer's style based on properties in the layer's source. For example, you might create a data-driven style rule that sets the color of states in the US based on the population of each state.

<div class='grid grid--gut6'>
  <div class='col col--6 pt12 pr12'>
    <strong>Get started with Mapbox GL JS expressions</strong>: In <a href='/help/tutorials/mapbox-gl-js-expressions/'>this tutorial</a>, each circle is a historical landmark. The size of the circle is the age of the landmark and zoom interpolation is used to create a smooth user experience.
  </div>
  <div class='col col--6'>
    <img class='mt0' src='/help/img/gl-js/mapbox-gl-js-expressions.png' alt='graduated circle map with circles of varying sizes'>
  </div>
  <div class='col col--6 pt12 pr12'>
    <strong>Choropleth map</strong>: In a choropleth map, a 'fill' layer changes color based on data properties.  In <a href='/help/tutorials/choropleth-studio-gl-pt-1/'>this tutorial</a>, the color of a state changes based on the population in the data.
  </div>
  <div class='col col--6'>
    <img class='mt0' class='fr' src='/help/img/screenshots/choropleth-160809.png' alt='choropleth map with each state in the United States colored according to a data property'>
  </div>
  <div class='col col--6 pt12 pr12'>
    <strong>Colored line map</strong>: In a colored line map, a line layer changes color based on data properties.  In this example, the color of a flight path changes based on the difference between local time at the flight's origin and destination.
  </div>
  <div class='col col--6'>
    <img class='mt0' class='fr' src='/help/img/screenshots/timezone-flights.png' alt='colored line map showing flight paths'>
  </div>
  <div class='col col--6 pt12 pr12'>
    <strong>3D Building map</strong>: Using a fill-extrusion layer, extrude buildings in 3D based on data properties. In <a href='https://www.mapbox.com/mapbox-gl-js/example/3d-buildings/'>this example</a>, the extrusion height of the building changes based on the "height" and "min_height" of the building polygon.
  </div>
  <div class='col col--6'>
    <img class='mt0' class='fr' src='/help/img/screenshots/3D_buildings_example_dds.png' alt='map showing 3D buildings where height is assigned according to a data property'>
  </div>
</div>

#### Required style sheet objects for data-driven styles

The value of any layout property, paint property, or filter within a style sheet may be specified as an expression. With [expressions](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions), you can style data with multiple feature properties at once, apply conditional logic, and manipulate data with arithmetic and string operations for a more sophisticated relationship between your data and how it is styled. Below is an example of the value of a layout property using a [match expression](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-match) to display a different icon image depending on the value of the `marker-number` property in the data -

```
"layout": {
  "icon-image": [
      "match", ["string", ["get", "marker-number"]],
        "one",
        "pin-red",
        "two",
        "pin-blue",
        "three",
        "pin-green",
        "pin-white"
      ],
  "icon-size": 1
}
```

The many types of expressions can be explored further within the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec) and in the examples like [Getting started with expressions](/help/tutorials/mapbox-gl-js-expressions/) and [Make a heatmap with Mapbox GL JS](/help/tutorials/make-a-heatmap-with-mapbox-gl-js/).

## Creating map styles

You can use the Mapbox Studio style editor to generate style JSON, write it directly, or use the Mapbox Styles API to read and change map styles, fonts, and images.

### Mapbox Studio

The Mapbox Studio style editor is a visual interface for creating and editing a style according to the Mapbox Style Specification. You can learn more about how to create and edit styles in the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/reference/styles/) style section.

### Cartogram

Use [Cartogram](https://apps.mapbox.com/cartogram/), a drag-and-drop tool, to create a custom map in seconds. Upload a picture, select the colors you want to use, and create a map style that fits your brand. Your new map style will be ready to use on a website or in a mobile application. You can also open it in the Mapbox Studio style editor to continue customizing the style or add custom data.

### Mapbox Styles API

The Mapbox Styles API lets you read and change map styles, fonts, and icons. This API is the basis for Mapbox Studio. If you use Mapbox Studio, Mapbox GL JS, or the Mapbox Mobile SDKs, you're already using the Styles API. You can learn more about the Styles API in our [API documentation](https://docs.mapbox.com/api/maps/#styles).

### Mapbox Style Specification

You can create a style from scratch using a text editor and following the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec).
