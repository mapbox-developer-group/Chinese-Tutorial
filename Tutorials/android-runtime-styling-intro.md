---
title: Runtime styling for Android
description: Change various properties of a map based on user interaction and other "runtime" situations.
thumbnail: androidRuntimeStyling
level: 2
topics:
- mobile apps
language:
- Java
prereq: An Android application with a map view set up and familiarity with Android Studio and Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-runtime-styling.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

[Runtime styling](/help/glossary/runtime-styling/) is a powerful feature within the Mapbox Maps SDK for Android, which enables you to change the map's properties in real time, allowing you to customize every aspect of the map’s appearance down to the smallest detail.

In this tutorial, you'll build a map for Android that changes the fill color of the earth's water and changes several text properties (size, color, halo blur, etc.) of marine labels.

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-dark-blue-water-adjusted-labels.png' alt='map with water fill color and marine label texts updated on an Android device' class='inline wmax360-mm wmax-full'>
</div>

## Getting started

This guide assumes that you are familiar with Java and Android Studio. Here are the resources that you’ll need before getting started:

- **A Mapbox account and access token**. Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account). You will add your access token to your strings.xml file.

- **An application including the Mapbox Maps SDK for Android.** This guide also assumes that you have already begun building an Android application that uses the Mapbox Maps SDK for Android. If you're new to the Maps SDK for Android, complete the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide to set up a map view first.


## Adding design library

Android Studio uses a toolkit called Gradle to compile resources and source code into an APK. The `build.gradle` file is used to configure the build and list dependencies, including the Mapbox Maps SDK for Android. In your `build.gradle` file, add the Android design support library as a dependency. This library isn't required to use runtime styling. It's being added to the app so that a floating action button can be used in this example.

```groovy
// in addition to the rest of your build.gradle contents
// you should include the following repository and dependency

repositories {
    mavenCentral()
}

dependencies {
    // Add other library dependencies such as the Mapbox Maps SDK for Android
    implementation 'com.android.support:design:27.1.1'
}
```

The `activity_main.xml` file is where you'll set the properties for your MapView and where you'll add a button to the layout. Clicking this button will trigger the runtime styling changes. In `app` > `res` > `layout` > `activity_main.xml`, specify the center of the map view, the zoom level, and the map style used when the application is initialized:

{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
  />
}}

You'll store your access token in the `strings.xml` file. In `app` > `res` > `values` > `strings.xml`:

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>strings.xml</div>
}}

```xml
<string name="access_token" translatable="false">{{ <UserAccessToken /> }}</string>
```

`MainActivity.java` is a Java file where you'll specify Mapbox-specific interactions. In `app` > `java` > `yourcompany.yourproject` > `MainActivity.java` initialize your map:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,11],
      [18,37],
      [58,105]
    ]}
  />
}}

You can learn how to set up an Android Studio project with the Maps SDK for Android in the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide. Run your application, and you should see a map in the Mapbox Streets style centered on the Gulf of Mexico and Caribbean Sea.

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-before.png' alt='a map centered on the Caribbean with Mapbox Streets style an Android device' class='wmax360'>
</div>


## Retrieve layers

Next, you'll use code from the Mapbox Maps SDK for Android to get the map's layers. Manipulating the layers is what leads to the visual changes.

### Import classes

First, import the correct classes in the `MainActivity.java` file. The `Layer` class is for creating layer objects that will be manipulated later. The `PropertyFactory` class enables you to change the map layers' colors and label properties.

Add the following code within the `public void onStyleLoaded(@NonNull final Style style) { ... }` method of the `MainActivity.java` file:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [13,13],
      [38,38]
    ]}
  />
}}

## Style the layers

Now you'll change the color of the water layer and several properties of marine labels text. In this tutorial, the changes will happen when the pink floating action button is clicked.

### Import classes

First, import the correct classes in the `MainActivity.java` file. The `View` class is for the pink floating action button's click listener. The `Color` class lets you use hex color codes to set the new color of the map layers.

### Change the water color

Start by adding the floating action button's click listener below the `waterLayer` Layer object. Then adjust the water color to a darker blue color inside of the `onClick()` method.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [15,16],
      [39,45],
      [57,57],
    ]}
  />
}}

Rerun your application, click on the pink floating action button, and you will see all the earth's water turn to a darker blue color.

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-dark-blue-water-only.png' alt='a map with dark blue colored water on an Android device' class='wmax360'>
</div>


### Change marine labels' text properties

Now specify the new properties of the water label text. In the floating action button's `onClick()` method, add the following code to adjust the labels' halo blur, size, color, and opacity.

The `for (Layer singleMapLayer : mapboxMap.getLayers())` line is used to tell the app to check each map layer for the text `water-`. This is because the Mapbox Streets style has several different water-related layer IDs:

- `water-point-label`
- `water-line-label`

Using the `for` loop allows you to retrieve these layers instead of creating a separate layer object for _each_ water label layer and then repeating the same text changes to each individual layer. With a `for` loop you can change the properties of several layers that have the same word in them. Examples of words that are commonly repeated in layer names are `building`, `water`, or `bridge`.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [46,55]
    ]}
  />
}}

{{<Note title='Layer IDs' imageComponent={<BookImage />}>}}

You will need the name (i.e. ID) of a layer if you'd like to change the layer's style at runtime. You can find the layer IDs for any map style (including our Mapbox template styles) by opening the style in Mapbox Studio. Make sure that you're signed into your Mapbox account and then visit the <a href='https://www.mapbox.com/studio/styles/'>Styles page</a>. Find the style in your account's list of styles and click on its Edit button. In the Mapbox Studio style editor, you will see the map style's layers listed in the left-hand sidebar.

Alternatively, you can use the [`getLayers()` method](https://www.mapbox.com/android-docs/api/map-sdk/{{constants.VERSION_ANDROID_MAPS}}/com/mapbox/mapboxsdk/maps/MapboxMap.html#getLayers) that is part of the `MapboxMap` class, to print the ID of each layer in your Android Studio Logcat console. Add the following `for` loop code within the `onMapReady` method of your `mapView` object to print the IDs:

```java
for (Layer singleMapLayer : mapboxMap.getLayers()) {
  Log.d("MainActivity", "onMapReady: layer name = " + singleMapLayer.getId());
}
```

Now that you have the full list of layer IDs, you will know what layers you'll be able to style in runtime!

{{ </Note> }}

Rerun your application, click on the pink floating action button, and you will see the map's water layers' text become much larger, greener, less opaque, and have a blurrier halo.

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-dark-blue-water-adjusted-labels.png' alt='map with attribute styled in runtime on an Android device' class='inline wmax360'>
</div>

## Finished product

You've created an app that changes the water layer's fill color and changes several text properties of multiple map layers. These changes didn't happen because of a particular data set, the map style, or any other factor. They happened in runtime and _on-the-fly_!

<div class='align-center'>
<img src='/help/img/android/android-runtime-styling-final.gif' alt='map with attribute styled in runtime on an Android device' class='inline wmax360'>
</div>

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## Next steps

There are many possibilities when using runtime styling to create beautiful and informative maps for Android applications. Read more about runtime styling more generally in our [Map design](/help/how-mapbox-works/map-design/) guide and dig into some runtime styling examples specifically for Android:

- [Switch map language](https://github.com/mapbox/mapbox-android-demo/blob/83a0b3c18f56cc549d68a28f23e3c2026e904e7c/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/styles/LanguageSwitchActivity.java): change the language of the map's text with the press of a button.
- [Update by zoom level](https://github.com/mapbox/mapbox-android-demo/blob/eadaf3a81c01f1390753dbe24b560f77d117ec27/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/styles/ZoomDependentFillColorActivity.java): change the color of the map's water layer based on the map's zoom level.
