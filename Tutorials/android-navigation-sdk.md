---
title: Build a navigation app for Android
description: Integrate navigation into any Android application.
thumbnail: androidNavigationSdk
level: 3
topics:
- mobile apps
- directions
language:
- Java
prereq: Familiarity with Android Studio and Java.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { AndroidTutorialCodeBlock } from '../../components/android-tutorial-code-block';"
  - "import * as snippet from '../../snippets/android-navigation-sdk.js'"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

The Mapbox Navigation SDK for Android gives you all the tools that you need to add turn-by-turn navigation to your apps. Get up and running in a few minutes with our drop-in turn-by-turn navigation, or build a more custom navigation experience with our navigation UI components.

<div class='align-center'>
<img alt="animated GIF of a navigation application where the user's location is shown on the map, the user clicks on the map, a route appears between the user's location and the clicked point, the user clicks start navigation to start the sequence with turn-by-turn instructions" class='inline wmax360-mm wmax-full' src='/help/img/android/nav-sdk-final-product.gif' >
</div>

## Getting started

The [Mapbox Navigation SDK for Android](https://www.mapbox.com/android-docs/navigation/overview/) runs on API 14 and above. The demo in this guide was built using API 26. Here are the resources you’ll need before getting started:

- **A Mapbox account and access token**. Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account/). You will add your access token to your strings.xml file.
- **An application including the Mapbox Maps SDK for Android.** This guide assumes that you have already begun building an Android application that uses the Mapbox Maps SDK for Android. If you're new to the Mapbox Maps SDK for Android, complete the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide to set up a map view first.

## Install the Navigation SDK

Before developing your app with the Mapbox Navigation SDK, you'll need to add several dependencies. Android Studio uses a toolkit called Gradle to compile resources and source code into an APK. The `build.gradle` file is used to configure the build and list dependencies. You should add the Navigation UI SDK as a dependency in the `repositories` section.

Declaring this dependency will automatically pull in both the Mapbox Navigation SDK for Android _and_ the Mapbox Maps SDK for Android. This is why the core Navigation SDK and Maps SDK dependency lines are not listed in the installation code snippet below. 

<!--copyeditor ignore best-->
We recommend not including an explicit version of the Maps SDK in your `build.gradle` file, because Gradle automatically takes care of adding the right dependencies. Instead, the Navigation SDK will include the Maps SDK versions that have been tested to provide the best user and developer experience for navigation apps. Manually adding a different Maps SDK version can lead to unexpected behavior.

In the module-level `build.gradle` file, add the following dependencies:

```groovy
// in addition to the rest of your build.gradle contents
// you should include the following repository and dependencies

repositories {
  mavenCentral()
  maven { url 'https://mapbox.bintray.com/mapbox' }
}

dependencies {
    implementation 'com.mapbox.mapboxsdk:mapbox-android-navigation-ui:{{constants.VERSION_ANDROID_NAV}}'
}
```

{{<Note imageComponent={<BookImage />}>}}
   
While we show how to insert the stable version of the SDK inside your project, you can also use the nightly build/SNAPSHOT or the beta version if one is available. Read more in the [GitHub repository](https://github.com/mapbox/mapbox-navigation-android#using-snapshots) for the Mapbox Navigation SDK for Android.

 
{{</Note>}}

## Initialize a map

Start by creating a new project in Android Studio and initializing a `MapView`.

Besides the `build.gradle` file where you installed the Navigation SDK, there are four files you'll use in Android Studio to set up a Mapbox map. The four files you'll be starting with include:

- **AndroidManifest.xml** (`app/manifests/AndroidManifest.xml`): This file is where you'll describe components of the application, including Mapbox-related permissions.
- **activity_main.xml** (`app/res/layout/activity_main.xml`): This is where you'll set the properties for your MapView including the map center, the zoom level, and the map style that will be used when the application is initialized.
- **strings.xml** (`app/res/values/strings.xml`): You'll update the name of the application and store your access token in this file.
- **MainActivity.java** (`app/java/yourcompany.yourproject/MainActivity.java`): In this Java file, you'll specify Mapbox-related interactions, starting by initializing your map.

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
    copyRanges={[
      [1,13]
    ]}
  />
}}

{{
  <div className="txt-s txt-fancy mb6" style={{ color: "#273d56" }}>strings.xml</div>
}}

```xml
<resources>
    <string name="app_name">Navigation map</string>
    <string name="access_token" translatable="false">{{ <UserAccessToken /> }}</string>
    <string name="user_location_permission_explanation">This app needs location permissions to show its functionality.</string>
    <string name="user_location_permission_not_granted">You didn\'t grant location permissions.</string>
</resources>
```

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [1,13],
      [48,51],
      [62,75],
      [97,98],
      [207,247]
    ]}
  />
}}


You can learn how to set up an Android Studio project with the Mapbox Maps SDK for Android in the [First steps with the Mapbox Maps SDK for Android](/help/tutorials/first-steps-android-sdk/) guide.

### Display user location

If you haven't configured location permissions already, you can use the [Mapbox `LocationComponent`](https://docs.mapbox.com/android/maps/overview/location-component/) to display the user's location on the map.

Showing a user's location requires importing several classes related both specifically to Mapbox and generally to location. Import the following classes below the classes you've already imported to your NavigationActivity file.

You'll also be using several variables throughout the process of adding a user's location to the map. Declare the following variables inside the NavigationActivity class below the existing variable, `private MapView mapView;`.

Now you are ready to enable the location component and display the user's location.

- You will also need to add two implementations to the NavigationActivity class: `LocationEngineListener` and `PermissionsListener`.
- Notice the updates to the `onStart`, `onStop`, and `onDestroy` methods.

{{
  <Note title='Location Layer component documentation' imageComponent={<BookImage />}>
    <p>If your app crashes or you run into other errors, make sure that you have enabled location permissions for this app on your physical or virtual device.</p>
    <p>Read more about the Location component including <a href='https://www.mapbox.com/android-docs/maps/overview/location-component/#customization'>various customization options</a> in the location component documentation.</p>
  </Note>
}}

Next, you'll call the `enableLocationComponent()` method when the map is finished loading. Add the following code after the code used to initialize the map.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [15,19],
      [52,54],
      [76,78],
      [96,96],
      [170,205]
    ]}
  />
}}

Run your application and you will see a circular "puck", which is the user's location on the map.

<div class='align-center'>
<img src='/help/img/android/nav-sdk-show-user-location.png' alt="an Android device displaying a map with a user's location" class='wmax360'>
</div>

### Add a marker on click

In this application, the user will be able to retrieve a route between their current location and any point that they select on the map. Next, you'll create the ability to add a marker to the map when the user taps on the map.

Start by importing the necessary classes for adding a marker to the map.

Then, add a few new variables that you will use to define the origin and destination based on the user's location and the selected point, respectively.


Now you are ready to add the code that will listen for when a user clicks on the map and then add a marker to the map.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [21,29],
      [80,82],
      [100,112],
      [114,125],
      [130,131]
    ]}
  />
}}

Run the application again. Click on the map, and you will see a marker added to the map.

<div class='align-center'>
<img src='/help/img/android/nav-sdk-add-marker.png' alt="an Android device displaying a user's location and marker on a map" class='wmax360'>
</div>


### Calculate and draw route

Next, you'll calculate and draw a route between the user's location and the newly added marker. First, import a set of classes required to calculate and draw a route on the map using the Mapbox Navigation SDK and the Mapbox Android Services Directions API wrapper.

Next, add a few more variables that you'll use while calculating and drawing the route.

Now you're ready to write a new `getRoute` method. This method will require a `origin` and `destination` to build a `NavigationRoute`. After passing an origin and destination to the method, you will make a request to the Mapbox Directions API. Once you've received a response, that response will be stored as the `currentRoute`. Then, you'll add `currentRoute` to your map. Start by checking if a route already exists on the map. If it does, remove it. Then, add the `currentRoute` to the map as a `NavigationMapRoute`.

Now you've written the `getRoute` method, but it still need to be called when the user adds a marker to the map. Call the `getRoute` method inside the `onMapClick() { ... });` method.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [31,40],
      [55,58],
      [127,127],
      [133,168]
    ]}
  />
}}

Run the application, click the map, and you will see a marker added to the map and a line displaying a route between the user's location and the clicked point.

<div class='align-center'>
<img src='/help/img/android/nav-sdk-calculate-and-draw-route.png' alt="an Android device displaying a map with a user's location, a marker, and a route between the two" class='wmax360'>
</div>

### Add a button to start navigation

Finally, you'll add a button and specify that when that button is clicked, a navigation interface should be displayed. Start by defining a few styles for the button. In the `colors.xml` file, add three new colors.

{{
  <AndroidTutorialCodeBlock
    filename="colors.xml"
    code={snippet.finalColors}
    copyRanges={[
      [1,3]
    ]}
  />
}}

Then, create a button in the `activity_main.xml` file. Use the colors you specified to set the `background` and `textColor`. Notice that when the application is first opened, the button will not be enabled (`android:enabled="false"`) and the button will be the `mapboxGrayLight` color.

{{
  <AndroidTutorialCodeBlock
    filename="activity_main.xml"
    code={snippet.finalLayout}
    copyRanges={[
      [15,28]
    ]}
  />
}}

Back in the NavigationActivity file, import the necessary classes for adding a button and opening a new navigation view.

Add a new variable for the button.

Then, add a button with a click listener. When the button is clicked, start the `NavigationLauncher`.

Finally, you'll need to specify that the button should change to be enabled after a marker is added to the map (when the `destination` is defined). You can accomplish this by setting the button to enabled and setting the background to the `mapboxBlue` color defined in the `colors.xml` file.

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
    copyRanges={[
      [42,45],
      [59,60],
      [83,95],
      [128,129]
    ]}
  />
}}

Run the application again. You should see a full width button at the top of the screen. Click a point on the map to add a marker and see an overview of the route. Then, click the **Start navigation** button to pull up the navigation view.

<div class='my12 grid grid--gut24'>
    <div class='col col--4-ml col--12 align-center'>
        <img alt="an Android device displaying a map, a user's location, and a button that is not enabled" src='/help/img/android/nav-sdk-add-button.png' class='wmax240'>
        <div><em>Before selecting a destination</em></div>
    </div>
    <div class='col col--4-ml col--12 align-center'>
        <img alt="an Android device displaying a map, a user's location, a marker, a route between the two, and an enabled button that says 'Start navigation'" src='/help/img/android/nav-sdk-add-marker-with-button.png' class='wmax240'>
        <div><em>After selecting a destination</em></div>
    </div>
    <div class='col col--4-ml col--12 align-center'>
        <img alt="an Android device displaying a navigation application with turn-by-turn instructions" src='/help/img/android/nav-sdk-start-navigation.png' class='wmax240'>
        <div><em>After clicking <strong>Start navigation</strong></em></div>
    </div>
</div>


## Customize the style

There are many ways to customize the appearance and functionality included in your navigation app. In this guide, you'll customize the colors to fit the Mapbox brand.

### Style the navigation view

First, change the style of the navigation view by changing colors to match Mapbox's brand. Define the following colors in the `colors.xml` file.

{{
  <AndroidTutorialCodeBlock
    filename="colors.xml"
    code={snippet.finalColors}
  />
}}

Then, specify the colors in the `styles.xml` file. The `NavigationMapRoute` style allows you change the appearance of the route on the map and the `NavigationView` style allows you to change the colors of the turn-by-turn instructions and progress bar.

{{
  <AndroidTutorialCodeBlock
    filename="styles.xml"
    code={snippet.finalStyles}
  />
}}

### Style the route overview

Next, change the color of the route overview that the SDK draws on the map when you click the map and add a marker. Find the code that is used to set the variable `navigationMapRoute` and replace it with the code below so the route will inherit the colors of the route in the navigation view.

```java
navigationMapRoute = new NavigationMapRoute(null, mapView, map, R.style.NavigationMapRoute);
```

Run the application, and you will see these changes applied to your app.

<div class='my12 grid grid--gut12'>
  <div class='col col--6-mm col--12 align-center'>
    <img alt="an Android device displaying a map, a user's location, a marker, a pink route between the two, and an enabled button that says 'Start navigation'" src='/help/img/android/nav-sdk-custom-route-overview.png' class='wmax360'>
    <div><em>Custom route overview style</em></div>
  </div>
  <div class='col col--6-mm col--12 align-center'>
    <img alt="an Android device displaying a navigation application with turn-by-turn instructions in Mapbox branded colors" src='/help/img/android/nav-sdk-custom-navigation-view.png' class='wmax360'>
    <div><em>Custom navigation view style</em></div>
  </div>
</div>

## Final product

You built a small navigation app with the Mapbox Navigation SDK for Android.

<div class='align-center'>
<img alt="animated GIF of a navigation application where the user's location is shown on the map, the user clicks on the map, a route appears between the user's location and the clicked point, the user clicks start navigation to start a navigation sequence with turn-by-turn instructions" class='inline wmax360-mm wmax-full' src='/help/img/android/nav-sdk-final-product.gif'>
</div>

Here's the code for the final MainActivity.java file:

{{
  <AndroidTutorialCodeBlock
    filename="MainActivity.java"
    code={snippet.finalJava}
  />
}}

## Next steps

There are many other ways you can customize the Mapbox Navigation SDK beyond what you've done in this tutorial. For a complete reference of customization options see the [Mapbox Navigation SDK for Android documentation](https://www.mapbox.com/android-docs/navigation/overview/).
