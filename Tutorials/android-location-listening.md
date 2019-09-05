---
title: Tracking device location for Android
description: Display a Mapbox map on an Android device and receive updates on the device's current location.
thumbnail: androidLocationTracking
level: 2
topics:
- mobile apps
language:
- Java
prereq: Familiarity with Android Studio and Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-location-tracking.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

The [Mapbox Core Libraries for Android](https://docs.mapbox.com/android/core/overview/) are a set of utilities, which help you with system permissions, device location, and connectivity within your Android project. These libraries help you with:

- Checking for, requesting, and responding to Android system location permissions.
- Checking for and responding to a change in the device's internet connectivity status.
- Retrieving a device's real-time location.

This tutorial will instruct you on how to add a Mapbox map to an Android app and then set up the Mapbox Core Libraries for Android to receive an update whenever a device's location changes. You will also use the Mapbox Maps SDK for Android's `LocationComponent` to display the device location icon. The information in a location change update includes the device's real-time coordinates, which can be helpful for your project.

By the end of this tutorial, you will have an app that displays [an Android system toast](https://developer.android.com/guide/topics/ui/notifiers/toasts) with the latest device location coordinates, whenever the Core library delivers a location update. Rather than showing a toast, you could use the coordinates how you'd like:

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-final.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>


## Getting started

Start by creating a new project in Android Studio and initializing a `MapView`. There are five files you'll be working with in your Android Studio project to set up a Mapbox map and add custom data to be styled using data-driven styling. The five files you'll be working with include:

- **build.gradle**: Android Studio uses a toolkit called Gradle to compile resources and source code into an APK. The `build.gradle` file is used to configure the build and list dependencies, including the Mapbox Maps SDK for Android.
- **AndroidManifest.xml**: The `AndroidManifest.xml` file is where you'll describe components of the application, including Mapbox-related permissions.
- **activity_main.xml**: The `activity_main.xml` file is where you'll set the properties for your `MapView` (for example, the center of the map view, the zoom level, and the map style used).
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
      [1,13],
      [31,38],
      [48,71],
      [73,75],
      [203,235],
      [240,247]
    ]}
  />
}}

You can learn how to set up an Android Studio project with the Maps SDK for Android in the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide.

Run your application, and you should see a map with the Mapbox Traffic Night style centered on Nashville, Tennessee, in the United States of America.

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-nashville-only.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>



## Handle location permissions

The Android system requires an app to be approved for device location tracking. The Mapbox Core Library helps to check for, request, and respond to the location permission request.

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-permission-dialog.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>

Using our static check, which returns a boolean, you can check if location permissions have already been requested. To make a location permission request, first implement the `PermissionsListener` interface.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [14,17],
      [39,40],
      [77,81],
      [111,111]
    ]}
  />
}}

Override the `onExplanationNeeded()` method once you implement the `PermissionsListener` interface.

Add a String resource titled `user_location_permission_explanation` in your `strings.xml` file, which will display if and when you need to provide further explanation for your location permission request.

```xml
<string name="user_location_permission_explanation">EXPLANATION_HERE</string>
```

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [128,136]
    ]}
  />
}}

The other method to override is `onPermissionResult()`. This convenient method will deliver you a true/false boolean value, which tells you whether a user accepted or denied the app's request to gain access to the device's location. Initialize the Maps SDK's `LocationComponent` once the location permission has been granted.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [138,141],
      [143,148]
    ]}
  />
}}

To start a permission check, create a new `PermissionManager` and call `requestLocationPermissions()`

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [82,83],
      [107,110]
    ]}
  />
}}


## Initialize the `LocationEngine`

Now that permissions have been handled, a `LocationEngine` object must be created and used.

Building a `LocationEngineRequest` is next. In the request, define:
- how many milliseconds you'd like to pass between location updates.
- how accurate you want the location updates to be.
- the maximum wait time in milliseconds for location updates. Locations determined at intervals but delivered in batch based on wait time. Batching is not supported by all engines.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [18,24],
      [41,44],
      [113,126]
    ]}
  />
}}

You'll also want to add the following to `onDestroy()` to prevent leaks:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [236,240]
    ]}
  />
}}


## Enable the `LocationComponent`

{{<Note imageComponent={<BookImage />}>}}
This section is optional. You can skip this section if you don't care about showing the location puck on the map.
{{</Note>}}

Thanks to the `PermissionsManager.areLocationPermissionsGranted(this)` boolean check, you now know that the location permission has been granted. You also know that the `LocationEngine` has been initialized. Now you can confidently initialize [the Maps SDK's `LocationComponent`](https://docs.mapbox.com/android/maps/overview/location-component/). The `LocationComponent` shows the device location "puck" icon on the map. You don't **have** to show the device location icon on the map to progress through this help guide. _Skip this section if you don't care about showing the location puck on the map_

The `LocationComponent` has `COMPASS` as its `RenderMode`, which means an arrow will be shown outside the location icon to display the device's compass bearing. The arrow indicates which direction the device is pointed towards. [There are other `RenderMode` choices if you do not want `COMPASS`](https://docs.mapbox.com/android/maps/overview/location-component/#rendermode).

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-compass-arrow.png' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>

The `LocationComponent` has `TRACKING` as its `CameraMode`, which means that the map camera will follow the device's location. [There are other `CameraMode` options though](https://docs.mapbox.com/android/maps/overview/location-component/#cameramode).

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [25,29],
      [72,72],
      [85,106],
      [142,142]
    ]}
  />
}}

## Listen to location updates

The last step is to create a location update interface callback to listen to location updates from the Mapbox Core Libraries for Android.

Create a class that implements `LocationEngineCallback<LocationEngineResult>`. The `LocationEngineCallback<LocationEngineResult>` interface is a part of the Core Libraries. Make sure the class requires Android system `Activity` as a constructor parameter. This new class should be created because a `LocationEngine` memory leak is possible if the activity/fragment directly implements the `LocationEngineCallback<LocationEngineResult>`. The `WeakReference` setup avoids the leak.

Implementing `LocationEngineCallback<LocationEngineResult>` requires you to override the `onSuccess()` and `onFailure()` methods.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [45,46],
      [150,201]
    ]}
  />
}}

`OnSuccess()` runs whenever the Mapbox Core Libraries identifies a change in the device's location. `result.getLastLocation()` gives you a `Location` object and that object has the latitude and longitude values. Now you can display the values in your app's UI, save it in memory, send it to your backend server, or use the device location information how you'd like.


## Finished product

You have set up code to be notified of device location updates. The screenshot below shows Nashville, but in reality, the map camera will move to wherever your device is if you're still using `TRACKING` as the `LocationComponent`'s `CameraMode`.

<div class='align-center'>
<img src='/help/img/android/android-location-tracking-final.gif' alt='map with location tracked and showing LocationComponent' class='inline wmax360-mm wmax-full'>
</div>

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## Next steps

There are many possibilities when using the `LocationComponent`. Explore [the Android demo app's location-related examples](https://github.com/mapbox/mapbox-android-demo/blob/master/MapboxAndroidDemo/src/main/java/com/mapbox/mapboxandroiddemo/examples/location/) to see how to show a device's location in an Android fragment, to customize the `LocationComponent` icon, and much more.
