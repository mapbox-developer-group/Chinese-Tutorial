---
title: Prototype apps with Mapbox in Framer X
description: Learn how to use the Mapbox component to add a map to a prototype in Framer X.
thumbnail: framerXMapboxComponents
topics:
- third party integration
level: 1
language:
- No code
prereq: Familiarity with Framer X.
prependJs:
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import * as constants from '../../constants';"
contentType: tutorial
---

The Mapbox component for [Framer X](https://framer.com/) allows designers to prototype location-aware products and apps, without needing to write any code. In this tutorial, you will learn how to use the Mapbox component to add a functional, data-rich map to a prototype in Framer X. This prototype will consist of three different frames, each using a different mapping function. The prototype will simulate an app that allows users to search, uses animations to display the search result, and then displays a list of local landmarks.

{{
<AppropriateImage imageId="framerXMapboxComponents" alt="Screenshot showing a prototype in Framer X that uses all three Mapbox components: Mapbox, SequentialLocationMap, and MarkerMap" />
}}

## Get started

There are a few resources you’ll need before you get started:

- **A Mapbox account and access token.** Sign up for a Mapbox account at [mapbox.com/signup](https://www.mapbox.com/signup/). Your access tokens are on your [Account page](https://www.mapbox.com/account).
- **A Framer account.** You need to have [Framer X](https://framer.com/) installed on your computer. You should also have some familiarity with how to use Framer X.

## Install the Mapbox component

This section assumes that you have a working knowledge of how to navigate and use Framer X. If you need help with Framer X, visit the [Framer documentation site](https://framer.com/docs/).

1. In Framer X, click on the **Store** icon.
1. Search for `Mapbox` in the search bar.
1. Select the Mapbox component, then click **Install**.

## Use the Mapbox component
For the first frame, you will use the **Mapbox** component to create a map with a functional search bar.

1. Once the Mapbox component has installed, click on the **Tools** icon.
1. Click the **Frame** button (or press the `F` key) to add a new frame to your project. The example in this tutorial uses the Apple iPhone 8 preset size. You can choose any preset frame size you like from the dropdown menus on the right side of the screen, or you can click and drag to create a freestyle frame.
1. Click on the **Components** icon. There are several component options: **`Mapbox`**, **`SequentialLocationMap`**, and **`MarkerMap`**.
1. Click on the `Mapbox` component and drag it onto the frame.
1. A new Mapbox map will populate inside the frame. You can resize and position the map within the frame.

{{
<AppropriateImage imageId="framerXAddMapboxComponent" alt="Screenshot showing how to add the Mapbox component to a Framer X prototype" class="mx-auto block" />
}}

### Add your Mapbox access token
The Mapbox component shows a functional map by default, but it also contains a text watermark in the upper left side of the map that says "Get your access token." When you add your access token, the text watermark will disappear.

1. Navigate to your [Mapbox account page](https://account.mapbox.com/). Click on the **clipboard icon** next to copy your _default public token_ to copy it.
1. In Framer X, paste this access token in the _Access Token_ field. Press the Enter key on your keyboard to integrate it into the current frame.

Next, you will change the map style to a Mapbox designer style.

{{
<AppropriateImage imageId="framerXAddAccessToken" alt="Screenshot showing how to add a Mapbox access token to Framer X" class="mx-auto block" />
}}

### Change the map style

The Mapbox component gives you access to several Mapbox core styles by default (Mapbox Light, Mapbox Dark, Mapbox Streets, Mapbox Satellite, and Mapbox Satellite Streets), and you can use these styles even if you do not add your access token. But to access any Mapbox designer styles, or a custom map style of your own creation, you will need to use your Mapbox access token, as described in the last section.

To change the map design:

1. In Framer X, click on the **Map Style** dropdown menu.
1. Click on the **LeShine** style.

The map in the Mapbox component will update to use the LeShine Mapbox designer style.

{{
<AppropriateImage imageId="framerXChangeMapStyle" alt="Screenshot showing where to change the map style in Framer X" class="mx-auto block" />
}}

### Update the map location

The Mapbox component comes with a list of default locations for you to use in your prototypes. You can also add a custom location if you choose.

1. Click the **City** dropdown menu.
1. Click on "Washington DC, USA".

The location shown in the map will change to Washington DC.

{{
<AppropriateImage imageId="framerXChangeLocation" alt="Screenshot showing where to change the city view in Framer X" class="mx-auto block" />
}}

### Add the search bar

Next, you will add the functional Mapbox search bar to this frame.

1. Click on the **Show** button next to the _Search_ option.
1. Use the _Position_ dropdown menu to move the bar to the top left side of the map.
1. Use the _Offset_ field to move the search bar down `15` pixels.
1. The _Drop Pin_ option is **True** by default. In this case, leave the setting as True since you want search results in your prototype to be marked with a pin.

{{
<AppropriateImage imageId="framerXAddSearchBar" alt="Screenshot showing how to add a search bar to the Mapbox component in Framer X" class="mx-auto block" />
}}

To preview this frame, click on the **Preview** icon on the top right side of the Framer X screen. In the Preview screen, you can type a location into the search bar and select a result. The map will fly to the selected location.

## Use the `SequentialLocationMap` component

Next, you will create a new frame using the **`SequentialLocationMap`** component. In this frame, you will prototype a search results screen that shows changes in pitch, bearing, and zoom.

1. Click the **Frame** button (or press the `F` key) to add another iPhone 8 frame to your project.
1. Click on the **Components** icon and drag the `SequentialLocationMap` component onto the new frame.
1. Paste your access token in the _Access Token_ field. Press the Enter key on your keyboard to integrate it into the current frame.
1. Click on the **Map Style** dropdown menu and choose the **LeShine** style.

### Set the map location

1. Click on the **Code** tab to expand it.
2. Click on the dropdown menu next to _File_ and select **New File**. (If prompted to do so, download Visual Studio Code.)
3. Framer X will open a `.tsx` file in Visual Studio Code. Delete the contents of this file and paste in the following code:
```js
import { Override } from "framer";

// To control what locations the map looks at, provide an
// array of location values. All properties for the locations are optional,
// with any unspecified values reverting to the current map's values.
// Valid properties are:
// latitude, longitude, zoom, bearing, pitch
export const CameraMoveSequence: Override = () => {
  return {
    locations: [
      // set the location to Sydney, Australia
      { bearing: 0, pitch: 0, zoom: 11, latitude: -33.86729979946806, longitude: 151.209683984967 },
      // zoom in to the location
      { zoom: 13 },
      // change the pitch of the map
      { pitch: 60 },
      // change the bearing of the map
      { bearing: 90 }
    ]
  };
};
```
4. Save the file. If you choose, you can rename the file using **Save As**, but the file must retain the `.tsx` extension.
5. In Framer X, click on the dropdown menu next to _File_ and select your new file.
6. Click on the dropdown menu next to _Override_ and select **`CameraMoveSequence`**.
7. Set the value of the _Autoplay_ field to **True**. This will start the animation automatically in Preview mode.

{{
<AppropriateImage imageId="framerXSetSequentialLocation" alt="Screenshot showing the how to set the locations for the SequentialLocationMap component in Framer X" class="mx-auto block" />
}}

To preview this frame, click on the **Preview** icon on the top right side of the Framer X screen. The preview will show Sydney and will move through the animations that you set up in the `.tsx` file.

## Use the `MarkerMap` component

Next, you will create a new frame using the **`MarkerMap`** component. In this frame, you will prototype a map that displays several marker locations.

1. Click the **Frame** button (or press the `F` key) to add another iPhone 8 frame to your project.
1. Click on the **Components** icon and drag the `MarkerMap` component onto the new frame.
1. Paste your access token in the _Access Token_ field. Press the Enter key on your keyboard to integrate it into the current frame.
1. Click on the **Map Style** dropdown menu and choose the **LeShine** style.

### Set the marker locations

The `MarkerMap` component requires a file with valid GeoJSON formatting to set the marker locations.

1. Open Visual Studio Code or the text editor of your choice.
1. Create a new file and name it `sydney_attractions.json`.
1. Paste the following code into the new file:
```js
[
  {
    "name": "Sydney Opera House",
    "location": { "longitude": 151.21507755097377, "latitude": -33.85725554523418 },
    "focusLocation": { "zoom": 9 },
    "category": "cultural attraction",
    "details": "World-famous opera house designed by Jørn Utzon. Opened in 1973."
  },
  {
    "name": "Bondi Beach",
    "location": { "longitude": 151.27362005956923, "latitude": -33.89084702828488 },
    "focusLocation": { },
    "category": "beach",
    "details": "A popular beach located in a Sydney suburb of the same name."
  },
  {
    "name": "Darling Harbour",
    "location": { "longitude": 151.20180875882124, "latitude": -33.87151653767559 },
    "focusLocation": { },
    "category": "cultural attraction",
    "details": "A large recreational and pedestrian precinct situated on the west side of the Sydney central business district."
  },
  {
    "name": "Sydney Harbour Bridge",
    "location": { "longitude": 151.21064244901527, "latitude": -33.8522736348907 },
    "focusLocation": { },
    "category": "cultural attraction",
    "details": "Distinctive bridge between the Sydney central business district and the North Shore. Opened in 1932. "
  },
  {
    "name": "Royal Botanical Gardens",
    "location": { "longitude": 151.21602755096444, "latitude": -33.86416527202888 },
    "focusLocation": { },
    "category": "cultural attraction",
    "details": "The oldest botanical garden in Australia. Opened in 1816."
  }
]
```
4. In Framer X, click the **Choose File** button next to the _Location_ option. Choose the `sydney_attractions.json` file.
5. Paste the longitude `151.2356` into the _Longitude_ field.
6. Paste the latitude `-33.8682` into the _Latitude_ field.
7. Change the value of _Zoom_ to `11`.
8. Click on the **Show** button next to the _Search_ option.
9. Use the _Position_ dropdown menu to move the bar to the top left side of the map.
10. Use the _Offset_ field to move the search bar down `15` pixels.

{{
<AppropriateImage imageId="framerXUpdateMarkerMapComponent" alt="Screenshot showing the how to set up the MarkerMap component in Framer X" class="mx-auto block" />
}}

To preview this frame, click on the **Preview** icon on the top right side of the Framer X screen. The preview will show Sydney and the markers set at each landmark described in `sydney_attractions.json`. If you click on a marker in Preview mode, it will display a card for the marker with information from the `.json` file's `name`, `category`, and `details` properties.

{{
<AppropriateImage imageId="framerXPreviewMarkerMapComponent" alt="Screenshot showing a preview of the MarkerMap component in Framer X" class="mx-auto block" />
}}

## Connect the frames

Finally, you will connect these three frames together so that they create one prototype.

1. Click the first frame. You will see a purple outline around the frame that shows that it is selected.
1. Click the purple circle on the right side of the frame and drag it so that it connects the first frame to the second.
1. To connect the second and third frames, you will create a button on the second frame. Click the **Frame** button (or press the `F` key) to add a new frame on top of the second frame. If you choose, you can adjust the location, size, color, and opacity of the new button using the controls on the right side of the screen. You can also add text to the button, such as "Show me places to visit!"
1. Select the button and type the `L` key to create a link. Drag the link and connect it to the third frame.

{{
<AppropriateImage imageId="framerXConnectFrames" alt="Screenshot showing the connected frames in Framer X" />
}}

## Finished product

You have created a prototype using the `Mapbox` component for Framer X. When you click the Preview button, you can see your new search app prototype. Type "Sydney" into the search bar and select the option "Sydney, New South Wales, Australia". The prototype will fly to Sydney and move through the animations you set in the `SequentialLocationMap` component. Then click on the button, which will pull up the markers that show the map locations you set in the `MarkerMap` component.

{{
<AppropriateImage imageId="framerXMapboxComponents" alt="Screenshot showing a prototype in Framer X that uses all three Mapbox components: Mapbox, SequentialLocationMap, and MarkerMap" />
}}

## Next steps
- For more tips on how to use Mapbox with Framer X, watch our tutorial videos on the [`Mapbox` component](https://www.mapbox.com/videos/how-to/install-and-use-mapbox-component-in-framer-x/), the [`SequentialLocationMap` component](https://www.mapbox.com/videos/how-to/install-and-use-sequentiallocationmap-component-in-framer-x/), and the [`MarkerMap` component](https://www.mapbox.com/videos/how-to/install-and-use-markermap-component-in-framer-x/).
- For information on how to create your own custom map styles that you can use in Framer X, read the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/overview/). You can also browse the Mapbox [style gallery](https://www.mapbox.com/designer-maps/) to get inspiration!
- Want to stay in the loop about what’s coming next in the Mapbox component for Framer X? Sign up on our [Framer X component page](https://mapbox.com/framerx).
