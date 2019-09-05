---
title: First steps with the Mapbox Maps SDK for iOS
description: Walk through installing the Mapbox Maps SDK for iOS, getting a map on the screen, and placing a pin on it.
thumbnail: firstStepsiOS
level: 1
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
  - "import { IosCodeToggle } from '../../components/ios-code-toggle'"
  - "import * as snippet from '../../snippets/first-steps-ios-sdk.js'"
contentType: tutorial
---


The [Mapbox Maps SDK for iOS](https://www.mapbox.com/ios-sdk) is our vector maps library for iOS. This guide will show you how to work with the Maps SDK for iOS, including how to customize your map, add markers with callouts, and display your user’s location on a map.

## Getting started

Before you begin, install the Mapbox Maps SDK for iOS by following our [installation guide](https://www.mapbox.com/install/ios/). You can integrate the Mapbox Maps SDK for iOS using a dependency manager such as Carthage or CocoaPods, or you can install the SDK manually.

After you complete the installation flow, your view controller should look like the one below if you chose the **“Add with code”** option. If you selected the **“Add with Storyboard”** option during the installation process, you will need to connect your [`MGLMapView`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html) to an `IBOutlet` so it is accessible within your view controller to continue with this guide.


{{
  <IosCodeToggle
    id='code-getting-started'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[8,11]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[13,16]]}
  />
}}


### Change the map style

To change your map style, set the [`MGLMapView.styleURL`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)styleURL) property to a [style URL](/help/glossary/style-url). This style URL can be any one of our beautiful [template](https://www.mapbox.com/maps/) or [designer styles](https://www.mapbox.com/designer-maps/), or you can create your own completely custom style in [Mapbox Studio](https://www.mapbox.com/studio-manual/).

The [`MGLStyle`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLStyle.html) class also provides a set of convenience methods that return the style URLs of [default Mapbox styles](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLStyle.html#/Accessing%20Default%20Styles).

For this guide, you will be using the Mapbox Satellite Streets style. Set the [`MGLMapView.styleURL`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)styleURL) property to the URL for this style using the provided convenience method, [`satelliteStreetsStyleURL`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLStyle.html#/c:objc(cs)MGLStyle(cm)satelliteStreetsStyleURL).

{{
  <IosCodeToggle
    id='code-change-the-map-style'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[13,13]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[18,18]]}
  />
}}

Then run your application to see the map's new style.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-satellite-style.png" className='wmax300' alt="Satellite map on iOS app" /></div>
</div>
}}

## Add a marker to the map

There are many ways to add a marker, also called an [annotation](/help/glossary/annotation/), to your map. `MGLPointAnnotation` provides the simplest way to add a predefined point style to your map.

Your `viewDidLoad` method should look like the code below to place a point annotation on Central Park within New York City.

{{
  <IosCodeToggle
    id='code-add-a-marker-to-the-map'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[15,20]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[20,25]]}
  />
}}

Run your application and notice the new point annotation added.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-add-marker.png" className='wmax300' alt="Map with marker on Central Park" /></div>
</div>
}}

`MGLPointAnnotation` is the base class of all point annotations and can be additionally configured to use views or static images in place of the default annotation style. Read the documentation for  [`MGLAnnotationView`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLAnnotationView.html) and [`MGLAnnotationImage`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLAnnotationImage.html) for more information about working with these types of annotations.

If you want to add a large number of points to a map, consider using runtime styling, which is another feature of the Mapbox Maps SDK for iOS geared towards creating rich data visualizations. For more information about the different ways to add points to a map and the differences between each approach, read our [Markers and annotations](https://www.mapbox.com/ios-sdk/maps/overview/markers-and-annotations/) guide.

### Add a callout

To get the annotation to display a callout when a user taps on it, the view controller will need to conform to the [`MGLMapViewDelegate`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Protocols/MGLMapViewDelegate.html) protocol to use the delegate methods `MGLMapViewDelegate` provides.

Once the view controller conforms to the `MGLMapViewDelegate` protocol and the map view's delegate is set to the view controller itself, you can then implement the <code><a href="https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:annotationCanShowCallout:">-mapView:annotationCanShowCallout:</a></code> delegate method. This makes sure that the map view knows that an annotation should display a callout when tapped. The full implementation of this is shown below:

{{
  <IosCodeToggle
    id='code-add-a-callout'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[22,23],[29,32]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[30,31],[34,37]]}
  />
}}


Run the application, and then try to tap the annotation &mdash; it now displays a callout with your annotation's `title` and `subtitle` when tapped!

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-add-callout.png" className='wmax300' alt="satellite map on iOS app" /></div>
</div>
}}

### Zoom to a marker

To center the map on the tapped marker, start by implementing the [`-mapView:didSelectAnnotation:`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:didSelectAnnotation:) delegate method. When the delegate method is called, initialize a new [`MGLMapCamera`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapCamera.html), which is the map's field of view. After creating the `MGLMapCamera`, call the [`-setCamera:animated:`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(im)setCamera:animated:) method on the `MGLMapView` to set the map's viewport to the new camera, which will be centered on the annotation's coordinate at a specified distance above ground level.

{{
  <IosCodeToggle
    id='code-zoom-to-a-marker'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[34,38]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[39,43]]}
  />
}}

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-zoom-marker.gif" className='wmax300' alt="zooming to marker" /></div>
</div>
}}

## Display the user’s location

If you haven't configured location permissions already, you will need to do so to use the device's location services. Before you can draw a user’s location on the map, you must ask for their permission and give a brief explanation of how your application will use their location data.

Configure location permissions by setting the `NSLocationWhenInUseUsageDescription` key in the Info.plist file. We recommend setting the value to the following string which is the application's location usage description: `Shows your location on the map and helps improve OpenStreetMap`. Additionally, you may also choose to include the `NSLocationAlwaysAndWhenInUseUsageDescription` within your Info.plist file. We recommend providing a different string when using this key to help your users decide which level of permission they wish to grant to your application. When a user opens your application for the first time, they will be presented with an alert that asks them if they would like to allow your application to access their location.

{{
<Note imageComponent={<BookImage />}>
  <p>If your application targets iOS 10 or below, you may also include the `NSLocationAlwaysUsageDescription` key your application. Note that this key is ignored in iOS 11.</p>
</Note>
}}

Once you have configured your application's location permissions, display the device's current location on the map by setting the [`showsUserLocation`](https://www.mapbox.com/ios-sdk/api/{{constants.VERSION_IOS_MAPS}}/Classes/MGLMapView.html#/c:objc(cs)MGLMapView(py)showsUserLocation) property on the map view to `true`.

{{
  <IosCodeToggle
    id='code-display-the-users-location'
    swiftCode={snippet.finalSwift}
    swiftCopyRanges={[[25,27]]}
    objectiveCCode={snippet.finalObjc}
    objectiveCCopyRanges={[[27,29]]}
  />
}}

### Simulating a location

When you run your app in Simulator, you’ll be presented with a dialog box asking for permission to use Location Services. Click **Allow**.

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-user-location-permission.png" className='wmax300' alt="Location permissions alert" /></div>
</div>
}}

You won’t see your location on the map until you go to Simulator’s menu bar and select **Debug ‣ Location ‣ Custom Location**. Enter `40.74699` for latitude, `-73.98742` for longitude, and you’re right outside Central Park in New York City!

{{
<div className='my12 p2 clearfix align-center'>
  <div className='device contain device-phone-v'><img src="/help/img/ios/first-steps-user-location.png" className='wmax300' alt="Map displaying user location" /></div>
</div>
}}

## Finished product

{{
  <IosCodeToggle
    id='code-finished-product'
    swiftCode={snippet.finalSwift}
    objectiveCCode={snippet.finalObjc}
  />
}}

## Next steps

You built a small app with the Mapbox Maps SDK for iOS! You added a Mapbox map to an iOS application, changed the map style, placed an annotation on your map, _and_ displayed the user’s location on it. Way to go!

As you continue to develop your Mapbox app, we recommend that you read the following:

* [Mapbox Maps SDK for iOS homepage](https://www.mapbox.com/ios-sdk) for general information about working with the Mapbox Maps SDK for iOS.
* [Mapbox Maps SDK for iOS documentation](https://www.mapbox.com/ios-sdk) for a complete reference of all classes and methods available.
* [Mapbox Maps SDK for iOS code examples](https://www.mapbox.com/ios-sdk) to see classes and methods in action.
* [Mapbox GL Native on GitHub](https://github.com/mapbox/mapbox-gl-native) to read about the open source project behind the Mapbox Maps SDK for iOS.
