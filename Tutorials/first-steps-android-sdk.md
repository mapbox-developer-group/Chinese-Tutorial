---
title: First steps with the Mapbox Maps SDK for Android
description: Walk through installing the Mapbox Maps SDK for Android, getting a map on the screen, and changing the map style.
thumbnail: firstStepsAndroid
level: 1
topics:
- mobile apps
language:
- Java
prereq: Completion of the Mapbox Maps SDK for Android installation process and familiarity with Android Studio and Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/first-steps-android-sdk.js'"
contentType: tutorial
---

The [Mapbox Maps SDK for Android](https://www.mapbox.com/android-sdk/) is our vector maps library for Android. This guide will walk you through installing the Mapbox Maps SDK for Android with [Android Studio](https://developer.android.com/studio/index.html), loading a map, changing the map's style, and placing a pin on it.

<div class='align-center'>
<img src='/help/img/android/android-first-steps-intro.png' alt='map with marker on an Android device' class='inline wmax360' />
</div>

## Getting started

Here's what you'll need to get started:

- **A Mapbox account and access token**. Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account/).
- **Android Studio**. You can download [Android Studio](http://developer.android.com/sdk/index.html) for free from Google. Before you can install the Mapbox Maps SDK for Android, you need to download Android Studio and create a project with an empty activity.
- **An Android device (physical or virtual)**. You will need either a physical Android device or an [emulated Android device](https://developer.android.com/studio/run/emulator.html) to preview the store finder.
- **Google Play Developer Account (optional)**. If you want to publish your app to Google Play, you'll need a [Google Play developer account](https://play.google.com/apps/publish/signup/). Without one, you'll still be able to preview the app on an Android Virtual Device (AVD) or install the app on a physical device.

### Create an Android Studio project

Familiarize yourself with Android Studio. You'll need to create a new project with an empty activity. Use the following options when creating a new Android Studio project:

- Under *Select the form factors your app will run on*, check "Phone and Tablet."
- For minimum SDK, `select API 14: Android 4.0.0 (IceCreamSandwich)`. (This is the lowest API level supported by Mapbox Maps SDK for Android.)
- Click **Next** to advance to the activity selection screen.
- Select **Empty Activity** and click **Next**.
- Accept the default `Activity Name` and `Layout Name` and click **Finish**.

If you need help installing Android Studio or creating your first project, see the [Android Studio documentation](https://developer.android.com/studio/intro/index.html).

### Set up a virtual device

With Android Studio, you can set up virtual Android devices on your computer to test your app while you develop. To set up a virtual device, click on the Android Virtual Device (AVD) Manager icon <img src="/help/img/android/first-steps-avd.png" alt='icon for AVD in the Android Studio interface' />, then click the **Create Virtual Device** button. You can also get to the manager via `Tools` > `Android` > `AVD Manager` in the toolbar. From the **Phones** category, select **Nexus 5X** and click **Next**. Select the release you would like to test against (this guide uses API level 26).

Learn more about setting up an AVD in the [Android Studio documentation](http://developer.android.com/tools/help/avd-manager.html).

## Install the Mapbox Maps SDK for Android

Before you begin building your app, install the Mapbox Maps SDK for Android by following our [installation guide](https://www.mapbox.com/install/android/). The installation guide assumes that you have already downloaded Android Studio and created a new project. You'll make changes to four different files within your project to install the Mapbox Maps SDK for Android. The four files you'll be working with include:

- `build.gradle (Module:App)`: Android Studio uses a toolkit called Gradle to compile resources and source code into an APK. This plain text file is used to configure the build and list dependencies, including the Mapbox Maps SDK for Android.
- `AndroidManifest.xml`: This is where you'll describe components of the application, including Mapbox-related permissions.
- `MainActivity.java`: This is a Java file where you'll specify Mapbox classes and methods.
- `activity_main.xml`: This is where you'll set the properties for your MapView and add a marker.

Once you've completed all the steps in the [installation guide](https://www.mapbox.com/install/android/), the four files below should include the following:

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>build.gradle (Module:App)</div>
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
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,12],
      [17,34],
      [50,97]
    ]}
  />
}}

{{
    <Note title='Troubleshooting Android Studio errors' imageComponent={<BookImage />}>
        <p>If you run into other Android Studio errors unrelated to Mapbox, we recommend referring to the <a href='https://developer.android.com/studio/intro/index.html'>Android Studio documentation</a> or searching for error messages on <a href='https://stackoverflow.com/questions/tagged/android-studio'>StackOverflow</a>.</p>
    </Note>
}}

### Configure your MapView

You can configure many of your map's characteristics, including starting camera position or the compass' location on the screen, in your activity's layout file. Replace the code you added to the `activity_main.xml` file in the installation flow with the following to recenter the map on Chicago, change the pitch, and increase the zoom level:

{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
  />
}}

The Mapbox Maps SDK for Android comes bundled with a handful of map styles. You can find a list of the current bundled styles with constants found in the Mapbox SDK's `Style` class.  In this example, you'll use the Mapbox Light style.

You _must_ the map style programmatically using the `MapboxMap` class' `setStyle();` method. Run `mapboxMap.setStyle()` within `onMapReady()`. The second parameter to pass through `setStyle()` is   the style loaded callback which is when the map is ready to receive map-related code:

```java
mapView.getMapAsync(new OnMapReadyCallback() {
@Override
public void onMapReady(@NonNull MapboxMap mapboxMap) {
mapboxMap.setStyle(Style.MAPBOX_STREETS, new Style.OnStyleLoaded() {
	  @Override
	  public void onStyleLoaded(@NonNull Style style) {
	    // Map is set up and the style has loaded. Now you can add data or make other map adjustments
	  }
	});
	}
});
```

You can also use `mapboxMap.setStyleUrl()` outside of the `onMapReady()` method:

```java
mapView.getMapAsync(new OnMapReadyCallback() {
  @Override
  public void onMapReady(MapboxMap mapboxMap) {
      MainActivity.this.mapboxMap = mapboxMap;
  }
});
```

The `MapboxMap` object near the top of your `MainActivity` is equal to the `MapboxMap` object that's returned once the map in your XML layout is ready. Now you can run `mapboxMap.setStyle()` anywhere else in your `MainActivity`'s code.

{{ <Note title='Creating your own styles' imageComponent={<BookImage />}> }}

<p>You can create custom styles with <a href='https://www.mapbox.com/mapbox-studio/'>Mapbox Studio</a> and then add them to your app. To programmatically add one of your custom styles to your <code>mapboxMap</code>, head to your <a href='https://www.mapbox.com/studio/styles/'>styles page</a>, copy your style's <a href='/help/glossary/style-url/'>style URL</a>, and then add it to your <code>mapboxMap</code> object with <code>setStyleUrl();</code>:</p>

```java
mapboxMap.setStyle(new Style.Builder().fromUrl("mapbox://styles/your-mapbox-username/your-style-ID"), new Style.OnStyleLoaded() {
  @Override
  public void onStyleLoaded(@NonNull Style style) {

  }
});
```

{{</Note>}}

See the [Mapbox Maps SDK for Android documentation](https://www.mapbox.com/android-docs/map-sdk/overview/#mapview-xml-attributes) to view all the XML attributes that you can set for a `MapView`. Customize your map to your heart's content!

### Import classes

When you've finished entering the above code, you will likely see some red warning text from Android Studio. This is because you haven't yet imported some of the classes that you're referencing in `MainActivity.java`.

You can automatically import these classes by pressing <kbd class='txt-kbd'>Alt</kbd>+<kbd class='txt-kbd'>Enter</kbd> (<kbd class='txt-kbd'>Option</kbd>+<kbd class='txt-kbd'>Return</kbd> on a Mac computer). Alternatively, you can manually add the following to the top of your `MainActivity.java` file, anywhere above the line that reads `public class MainActivity extends AppCompatActivity`:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [13,15]
    ]}
  />
}}

Click the **Run 'app'** button <img src="/help/img/android/first-steps-run.png" alt="icon for running the app in Android Studio" />(or <kbd class='txt-kbd'>Control</kbd>+<kbd class='txt-kbd'>R</kbd> on a Mac computer) to build your app.

Android Studio will take a few seconds to build, and if it finishes without errors, you'll be able to test drive it in the emulated Android device that you set up earlier. Regardless of the approach you take, the result should be the same &mdash; you should see the initial map style replaced with the Mapbox Light style.

<div class='align-center'>
<img src='/help/img/android/first-steps-change-style.png' alt='screenshot of a virtual Android device displaying a map using the Mapbox Light style' class='inline wmax360'>
</div>

## Add a marker

Next, you'll add a marker to your map. In your `MainActivity.java` file, add the following code immediately after `mapView.onCreate(savedInstanceState);`, but still within `public void onStyleLoaded(@NonNull Style style) { ...});`. This will wait until the map has loaded, and then add a single marker displayed at the specified coordinate.

Once the style has been to set to Mapbox Light, you will add an icon image to the map and then use that icon when you add a `SymbolLayer` to the map.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [35,48]
    ]}
  />
}}

Rerun your application and a red marker should appear.

<div class='align-center'>
<img src='/help/img/android/android-first-steps-intro.png' alt='map with marker on an Android device' class='inline wmax360'>
</div>

## Final product

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## Next steps

You built a small Android app with Mapbox! You can now create an Android Studio project, install the Mapbox Maps SDK for Android, and change the map style. Here are a few resources to keep you up-to-date with Mapbox:

* [Mapbox Maps SDK for Android documentation](https://docs.mapbox.com/android/maps/overview)
* [Mapbox Maps SDK for Android examples](https://docs.mapbox.com/android/maps/examples)
* [Mapbox GL Native on GitHub](https://github.com/mapbox/mapbox-gl-native) to follow the open source project behind Mapbox Mobile

You can also [download and explore our Android demo app](https://play.google.com/store/apps/details?id=com.mapbox.mapboxandroiddemo&hl=en) to see all the ways that you can use Mapbox in your Android project.
