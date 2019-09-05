---
title: Data-driven styling for Android
description: Create a map for Android that styles a circle based on a data attribute.
thumbnail: androidDdsCircleLayer
level: 2
topics:
- mobile apps
language:
- Java
prereq: An Android application with a map view set up and familiarity with Android Studio and Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-dds-circle-layer.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

[Data-driven styling](/help/glossary/data-driven-styling/) is a powerful feature within the Mapbox Maps SDK for Android that allows you to use data attributes to style your maps. With data-driven styling, you can automatically style map features based on their individual attributes. In this tutorial, you'll build a map for Android that includes a circle layer styled based on a data attribute.

<div class='align-center'>
<img src='/help/img/android/android-dds-style-by-attribute.png' alt='map with data styled by attribute on an Android device' class='inline wmax360-mm wmax-full'>
</div>

## Getting started

This guide assumes that you are familiar with Java and Android Studio. Here are the resources that you’ll need before getting started:

- **An application including the Mapbox Maps SDK for Android.** This guide also assumes that you have already begun building an Android application that uses the Mapbox Maps SDK for Android. If you're new to the Maps SDK for Android, complete the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide to set up a map view first.
- **Data.** We collected data from the District of Columbia's [Open Data DC](http://opendata.dc.gov/) that shows the location of street trees in Washington, D.C. Each tree has a `DBH` attribute that is the [diameter at breast height](https://en.wikipedia.org/wiki/Diameter_at_breast_height), a common metric for expressing the size of trees.

{{
<Button href="/help/data/street-trees-DC.zip" passthroughProps={{ download: "street-trees-DC" }} >
    <Icon name='arrow-down' inline={true} /> Download Shapefile
</Button>
}}

## Upload data to Mapbox

In this tutorial, you will be using a [vector tileset](/help/glossary/tileset) to display data in your application. You can create a vector tileset by uploading the Open Data DC Shapefile Mapbox Studio:

1. Log into [Mapbox Studio](https://www.mapbox.com/studio).
1. Visit the [Tilesets page](https://www.mapbox.com/studio/tilesets).
1. Click **New tileset**.
1. Select the Shapefile you downloaded at the beginning of this tutorial and click **Confirm**.
1. A popover will appear in the bottom right showing the progress of your upload.
1. Once the upload has _Succeeded_, the tileset will be ready to use! Click on the name of the tileset in the popover, which will open the tileset information page.
1. Take note of the **tileset ID** on the right side of the tileset information page. You will use the ID to add this tileset to your application later in this guide.

## Initialize a MapView

Start by creating a new project in Android Studio and initializing a MapView. There are five files you'll be working with in your Android Studio project to set up a Mapbox map and add custom data to be styled using data-driven styling. The five files you'll be working with include:

- **build.gradle**: Android Studio uses a toolkit called Gradle to compile resources and source code into an APK. The `build.gradle` file is used to configure the build and list dependencies, including the Mapbox Maps SDK for Android.
- **AndroidManifest.xml**: The `AndroidManifest.xml` file is where you'll describe components of the application, including Mapbox-related permissions.
- **activity_main.xml**: The `activity_main.xml` file is where you'll set the properties for your MapView (for example, the center of the map view, the zoom level, and the map style used).
- **strings.xml**: You'll store your access token in the `strings.xml` file.
- **MainActivity.java**: `MainActivity.java` is a Java file where you'll specify Mapbox-specific interactions.

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>build.gradle (App module)</div>
}}

```groovy
// in addition to the rest of your build.gradle contents
// you should include the following repository and dependency
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.mapbox.mapboxsdk:mapbox-android-sdk:{{constants.VERSION_ANDROID_MAPS}}'
}
```

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>Manifest.xml</div>
}}

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```



{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
  />
}}

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>strings.xml</div>
}}

```xml
<string name="access_token" translatable="false">{{ <UserAccessToken /> }}</string>
```

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,10],
      [23,40],
      [63,67],
      [70,111]
    ]}
  />
}}

You can learn how to set up an Android Studio project with the Maps SDK for Android in the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide.

Run your application, and you should see a map in the Mapbox Dark style centered on Logan Circle.

<div class='align-center'>
<img src='/help/img/android/android-dds-initialize-map.png' alt='initialized map on an Android device' class='wmax360'>
</div>

## Load the source

Next, you'll load the tileset that you added to your Mapbox Studio account into the application using the [tileset ID](/help/glossary/tileset-id). Find your tileset ID on the [Tilesets page in Mapbox Studio](https://www.mapbox.com/studio/tilesets/) by clicking the {{<Icon name='menu' inline={true} />}} next to the tileset you uploaded.

First you'll need to import the correct classes in the `MainActivity.java` file. This will allow you to add a vector source and create a circle layer from that data.

Then, add the code that pulls in the data in your tileset and adds it as a layer to your map. In the `MainActivity.java` file, inside `public void onStyleLoaded(@NonNull Style style) { ... }` add the following code:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [12,13],
      [41,50],
      [62,62]
    ]}
  />
}}


Rerun your application and you'll see the data from your tileset displayed on the dark map. Notice that the black circles are difficult to see on top of the dark map style. Next, you'll style the data to be more visible.

<div class='align-center'>
<img src='/help/img/android/android-dds-load-data.png' alt='map with data on an Android device' class='wmax360'>
</div>

## Style the layer

Now you'll change the color and opacity of each circle to make the data more visible against the dark map style. Then, you'll also change the size of each circle to reflect the `DBH`.

### Change color and opacity

Start by importing the correct classes in the `MainActivity.java` file. In this step you'll need the `circleColor` and `circleOpacity` classes.

Then, add the following code to the inside the `public void onStyleLoaded(@NonNull Style style) {...}` method to specify the opacity and color that the layer should use:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [15,16],
      [51,53],
      [61,61]
    ]}
  />
}}

Rerun your application, and you will see the same map view with the same point data, but now the circles will be white and semi-transparent.

<div class='align-center'>
<img src='/help/img/android/android-dds-color-opacity.png' alt='initialized map on an Android device' class='wmax360'>
</div>


### Specify radius based on a data attribute

Finally, you'll specify that the radius of circle should be determined by the `DBH` value. Again, you'll start by importing the necessary classes. You'll need the `Function` and `exponential` classes to create a property function, the `Stop` class to establish what the circle radius should be at which `DBH`, and the `circleRadius` class to affect the circleRadius paint property.

Then, replace the code used to specify paint properties for the layer, inside `circleLayer.withProperties( ... )`, to use an exponential property function:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [17,21],
      [54,60]
    ]}
  />
}}

Rerun your application, and you will see the map with your data styled in a way that the radius of each circle is determined by the `DBH` value for that point.

<div class='align-center'>
<img src='/help/img/android/android-dds-style-by-attribute.png' alt='map with data styled by attribute on an Android device' class='inline wmax360'>
</div>

## Finished product

You've created a data visualization that illustrates the location and size of street trees all over Washington DC.

<div class='align-center'>
<img src='/help/img/android/android-dds-final-product.gif' alt='map with data styled by attribute on an Android device' class='inline wmax360'>
</div>

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## Next steps

There are many possibilities when using data-driven styling to create beautiful and informative data visualizations for Android applications. Read more about data-driven styling more generally in our [Map design](/help/how-mapbox-works/map-design/) guide and dig into some data-driven styling examples specifically for Android:

- [Style circles categorically](https://github.com/mapbox/mapbox-android-demo/blob/master/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/dds/StyleCirclesCategoricallyActivity.java): change the color of circles in a circle layer based on a data property.
- [Update by zoom level](https://github.com/mapbox/mapbox-android-demo/blob/master/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/dds/ChoroplethZoomChangeActivity.java): display state or county population depending on zoom level.
