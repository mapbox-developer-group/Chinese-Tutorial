---
title: Get started with expressions using the Mapbox Maps SDK for iOS
description: Create a map for iOS that styles a circle based on a data attribute.
thumbnail: iosDdsCircleLayer
level: 2
topics:
- mobile apps
language:
- Swift
- Objective-C
prereq: Familiarity with Xcode and either Swift or Objective-C, and completion of the Mapbox Maps SDK for iOS installation guide.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { IosCodeToggle } from '../../components/ios-code-toggle'"
  - "import * as snippet from '../../snippets/ios-dds-circle-layer.js'"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

In this guide you’ll learn how to write expressions using the Mapbox Maps SDK for iOS to style custom data based on a data attribute and by zoom level.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-post-zoom-expression.png' alt='adjust the circle radius based on zoom level' /></div>
</div>
}}

## Getting started

This guide assumes you are familiar with Objective-C or Swift. Here are the resources you’ll need before getting started:

- **An application including the Mapbox Maps SDK for iOS.** This guide also assumes that you have already set up an `MGLMapView` with the Mapbox Maps SDK for iOS. If you're new to the Maps SDK for iOS, complete the [First steps with the Mapbox Maps SDK for iOS](/help/tutorials/first-steps-ios-sdk/) guide to set up a map view first.
- **Data**. In this tutorial, you'll be using a CSV file of [HPC Landmarks from Open Minneapolis](http://opendata.minneapolismn.gov/datasets/hpc-landmarks/data).

{{
<Button href="/help/data/trees.geojson" passthroughProps={{ download: "trees.geojson" }} >
    <Icon name='arrow-down' inline={true} /> Download the data
</Button>
}}

## What are expressions?

In the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec/), the value for any layout property, paint property, or filter may be specified as an expression. Expressions define how one or more feature attribute values and/or the current zoom level are combined using logical, mathematical, string, or color operations to produce the appropriate style property value or filter decision.

The Mapbox Maps SDK for iOS allows you create expressions that follow the Mapbox Style Specification standard by using [`NSExpression`](https://developer.apple.com/documentation/foundation/nsexpression). In this tutorial, you'll create both property and zoom expressions to conditionally change a layer's style.

A **data expression** is any expression defined using a reference to feature property data. Property expressions allow the appearance of a feature to change with its properties. They can be used to visually differentiate types of features within the same layer or create data visualizations.


{{
  <Note title='Migrating from earlier Maps SDK versions (<4.0.0)' imageComponent={<BookImage />}>
    <p>If you've styled your data at runtime in the past with older versions of the Mapbox Maps SDK for iOS, read our <a href="https://www.mapbox.com/ios-sdk/api/{constants.VERSION_IOS_MAPS}/migrating-to-expressions.html">migration guide</a> to learn more about switching your style functions to expressions.</p>
  </Note>
}}

## Uses
There are countless ways to apply property expressions to your application, including:

- **Data-driven styling**: Specify style rules based on one or more data attribute, such as coloring state polygon based on their population.
- **Arithmetic**: Do arithmetic on source data, for example performing calculations to convert units dynamically.
- **Conditional logic**: Use if-then logic, for example to decide exactly what text to display for a label based on which properties are available in the feature or even the length of the name.
- **String manipulation**: Take control over label text with things like uppercase, lowercase, and title case transforms without having to edit, re-prepare and re-upload your data.

In this tutorial, you'll learn how to use expressions to style Historic Preservation Commission landmarks in Minneapolis based on age and zoom level.

## Set up a map

### Initialize a map view

To begin building your data visualization, you first need to initialize a map view. Use the code below to create a map view that uses the [Mapbox Light](https://www.mapbox.com/maps/light-dark/) style and is centered on Minneapolis, Minnesota:

{{
  <IosCodeToggle
    id='code-initialize-a-map-view'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[6,17]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[9,22]]}
  />
}}


The result will be a blank map using the Mapbox Light style, as shown below:

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-simple-mapview.png' alt='blank light map on an iOS device' /></div>
</div>
}}

### Upload data

In this guide, you'll use a [vector tileset](/help/glossary/tileset) to display data in your application. You can create a vector tileset by uploading the CSV you downloaded earlier to Mapbox Studio:

1. Visit the [Tilesets page](https://www.mapbox.com/studio/tilesets) in Mapbox Studio.
1. Click **New tileset**.
1. Select the CSV you downloaded at the beginning of this tutorial and click **Confirm**.
1. A popover will appear in the bottom right showing the progress of your upload.
1. Once the upload has _Succeeded_, the tileset will be ready to use! Click on the name of the tileset in the popover, which will open the tileset information page.
1. Take note of the *tileset ID* on the right side of the tileset information page. You will use the ID to add this tileset to your map in the next step.

### Add the source data to the map

To load the data onto the map, you'll need to do two things:

1. Add the vector tileset to the map dynamically as an [`MGLVectorTileSource`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLVectorTileSource.html) to initially load the source data.
2. Add a corresponding `MGLCircleStyleLayer` that references the above `MGLVectorTileSource` to display the data on the map.

The source data and style layer should be added after the map is finished loading, so the code to both should reside within the {{<a href="https://www.mapbox.com/ios-sdk/api/{constants.VERSION_IOS_MAPS}/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:didFinishLoadingStyle:"><code className="highlighter-rouge">-mapView:didFinishLoadingStyle:</code></a>}} delegate method.

{{
  <IosCodeToggle
    id='code-add-the-source-data-to-the-map'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[19,31],[40,41]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[25,37],[46,47]]}
  />
}}

When you run your application, you'll see that the tileset has been added as a source to the map. You can now see circles marking where each landmark is with an assigned circle color and opacity.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-add-source.png' alt='adding a new circle layer to a map' /></div>
</div>
}}

### Use an expression to calculate the age of each landmark

Next, you’ll write an expression to style the radius of each circle based on the age of each historic landmark. In this data file, provided by the City of Minneapolis’s open data portal, the age of the historic landmark is not provided, but the year of construction is provided.

Instead of manually editing your source data and re-uploading it, you can use arithmetic to calculate the age of each landmark based on the current year. Once the age of each landmark has been calculated, you can style the [`circleRadius`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLCircleStyleLayer.html#/c:objc(cs)MGLCircleStyleLayer(py)circleRadius) paint property based on the calculated age of each landmark.

Start by calculating the age of the landmark and assigning it as the circle's radius, such that older landmarks will have a larger circle radius.

```swift
layer.circleRadius = NSExpression(format: "2018 - Constructi")
```

```objectivec
layer.circleRadius = [NSExpression expressionWithFormat:@"2018 - Constructi"]
```

The above expression subtracts the current year (2018) each feature's date of construction. `Constructi` is the name of the key corresponds to the year each landmark was constructed. Run the application again to see the changes.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-calculate-age.png' alt='change the radius of each circle based on the age of each landmark' /></div>
</div>
}}

Wow! Those circles are quite large. This is because a radius is measured in screen points, whereas `Constructi` is measured in years. To make this look better, you'll make some adjustments to the circle radius.

### Adjust the circle radius

Since expressions can support mathematical operations, you can take the existing expression and divide the age by 10 to reduce the radius of each circle.

```swift
layer.circleRadius = NSExpression(format: "(2018 - Constructi) / 10")
```

```objectivec
layer.circleRadius = [NSExpression expressionWithFormat:@"(2018 - Constructi) / 10"]
```

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-reduce-circle-radius.png' alt='reduce the size of each circles radius' /></div>
</div>
}}

That looks better! Reducing the size of the circles makes this map much more legible at this zoom level. There are still some circles overlapping at this zoom level, so lets add a zoom expression to adjust the radius of the circles based on the zoom level the map is at.

### Add a zoom expression

The circles are still overlapping quite a bit at the starting zoom level of 10, but they look good at higher zoom levels. You can use a zoom expression to address this issue, which will allow the appearance of a layer to change with the map’s zoom level. Zoom expressions can be used to create the illusion of depth and control data density.

You will create a new linear interpolation expression to define a different circle radius between the following zoom levels:

| Zoom level | Circle radius    |
|------------|------------------|
| 0-10       | Calculated building age ÷ 30 |
| 13+        | Calculated building age ÷ 10 |

By using a linear interpolation, the circle radius will stay the same between categories. For example, at zoom level 18 the circle radius will still be the building age, divided by 10. There are other types of interpolations that would interpret this differently, which you can read about in more detail within the [Maps SDK documentation](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Categories/NSExpression%28MGLAdditions%29.html#/c:objc(cs)NSExpression(cm)mgl_expressionForInterpolatingExpression:withCurveType:parameters:stops:).

Within your code, the linear interpolation expression will look like this:

{{
  <IosCodeToggle
    id='code-calculate-add-a-zoom-expression'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[33,39]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[39,44]]}
  />
}}

{{
  <Note imageComponent={<BookImage />}>
    <p>If you've worked with <a href='https://www.mapbox.com/mapbox-gl-js/style-spec/#types-function'>property <em>functions</em></a> before, notice that <code>MGLInterpolationModeExponential</code> expressions allow you to achieve the same effect as using an `MGLStyleValue` with source stops.</p>
  </Note>
}}

Once you run your application again, you'll notice that at the same zoom level, the circles appear more distinct.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'><img src='/help/img/ios/ios-dds-circle-layer-post-zoom-expression.png' alt='adjust the circle radius based on zoom level' /></div>
</div>
}}

## Finished product

You’ve styled custom data using expressions using the Mapbox Maps SDK for iOS!

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-h'>
    <video autoPlay loop width="100%" className="block" src='/help/img/ios/ios-dds-circle-layer-result.mp4' type='video/mp4'></video>
  </div>
</div>
}}

You can find the completed code for this tutorial below.

{{
  <IosCodeToggle
    id='code-finished-product'
    swiftCode={snippet.finalSwift}
    objectiveCCode={snippet.finalObjc}
  />
}}
