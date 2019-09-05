---
title: Create a timezone finder with Mapbox Tilequery API
description: Create a timezone finder app with Mapbox Tilequery API.
thumbnail: createATimezoneFinderWithMapboxTilequeryApi
topics:
- data
- web apps
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts including JavaScript and API calls.
prependJs:
  - "import * as constants from '../../constants';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

The Mapbox Tilequery API enables users to get data from a tileset without necessarily needing to render a map. This tutorial shows you how to create an  app that uses the Tilequery API and a custom tileset to determine which timezone a user is in.

{{
  <DemoIframe gl={false} src="/help/demos/tilequery-intro/index.html" />
}}

You will not be building a map in this tutorial. To see an example of how Mapbox Tilequery API can be used to interact with a rendered map, take a look at the [Tilequery API Playground](/help/interactive-tools/tilequery-api-playground).

## Getting started

There are a few resources you’ll need before getting started:

- **An access token** from your Mapbox account. You will use an access token to associate a map with your account. Your access token is on the  [Account page](https://account.mapbox.com/).
- **Data.** Your app will reference a tileset that contains timezone information.
  - This data set was sourced from [Evan Savage](https://github.com/candu/efele-tz-world-geojson)’s GitHub. For this tutorial, you don't have to download the data or upload it to Mapbox &mdash; we've done that for you already!
  - Normally, you would need to upload this data to Mapbox using either [Mapbox Studio](https://www.mapbox.com/studio/tilesets/) or the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads).
- **Mapbox Tilequery API.** Our [Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) lets you query custom data without needing to render a map to the page.
- **jQuery.** [jQuery](https://jquery.com/) is a JavaScript library you will use to add your API request to your application.
- **Assembly.** [Assembly](https://labs.mapbox.com/assembly/) is an open source CSS framework that is maintained by Mapbox.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.

In this tutorial, you will create an interface using HTML and style it using Assembly, the CSS framework that Mapbox uses. Then you will add a call to the native HTML geolocation API, as well as a call to the Mapbox Tilequery API to query a custom tileset that contains timezone data. At the end of this tutorial, you will have created an app that, when a user clicks a button, determines their timezone.

## Structure the webpage

Start by pasting the following code into your text editor. This code references a few items in the `<head>` of your file that you will take advantage of later in this tutorial:

- **jQuery.** Used to make the Tilequery API call and parse the response.
- **Assembly.** Using this framework will allow you to add styles to the HTML without having to write custom CSS.

```html
<!DOCTYPE html>
<html>

  <head>
    <meta charset='utf-8' />
    <title></title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <!-- import jQuery -->
    <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js'></script>
    <!-- import Assembly JavaScript -->
    <script async defer src='https://api.mapbox.com/mapbox-assembly/v0.21.2/assembly.js'></script>
    <!-- import Assembly CSS -->
    <link href='https://api.mapbox.com/mapbox-assembly/v0.21.2/assembly.min.css' rel='stylesheet'>
  </head>

  <body>
    <!-- the Assembly classes in the div below create a centered div with a top margin of 36px -->
    <!-- read the Assembly documentation for more info!   -->
    <div class='mx-auto mt36 w600 prose'>
      <h2>Timezone finder</h2>
      <button id='tz-button' class='btn'>Find my timezone!</button>
      <!-- the textContainer div will display the success, error, and loading messages -->
      <div class='mt12 ml12' id='textContainer'>
        <!-- these Assembly classes will add an animation to the loading message! -->
        <p id='loading-message' class='inline-block round animation-pulse animation--infinite'></p>
        <p id='return-message'></p>
      </div>
    </div>

  </body>

</html>
```

Save this file and open it in your browser. The `body` of the code references a few different Assembly classes, so you do not need to add any additional styles (unless you want to!).

<img alt="a screenshot showing the interface of the Tilequery API timezone finder app" src='/help/img/api/tilequery-timezone-finder.png' class='block wmax600 mx-auto'>

This code doesn't do anything yet, so in the next few steps you will add more functionality to turn it into a fully realized timezone finder.

## Build the API request

Next, you will build your request to the Mapbox Tilequery API and test it in your browser. After you have verified that it is returning the expected results, you will add the API call to your app!

The format of a Tilequery API call is:

```
https://api.mapbox.com/v4/{tileset}/tilequery/{longitude},{latitude}.json?access_token={{ <UserAccessToken /> }}
```

In a Mapbox Tilequery API call, the tileset indicates the data that your API request will be querying. In this case, your app will query custom data that has been uploaded to Mapbox. You will reference this [tileset id](/help/glossary/tileset-id/) (`examples.4ze9z6tv`) in the API call. You can also tell the Tilequery API to ask questions of Mapbox’s default tilesets, such as [Mapbox Streets](https://www.mapbox.com/studio/tilesets/mapbox.mapbox-streets-v7/) or [Mapbox Terrain](https://www.mapbox.com/studio/tilesets/mapbox.mapbox-terrain-v2/). To visualize the results of a call to one of these tilesets, use the [Tilequery API Playground](/help/interactive-tools/tilequery-api-playground).

### Parameters

The only required parameters for a call to the Mapbox Tilequery API are the longitude and latitude of a desired location. To test the API, we will set this to `-77.033835,38.89975`, the coordinates of Mapbox’s Washington D.C. office.

The Tilequery API also accepts several optional query parameters, including *radius*, that you will not need to use for this project. Read more about these optional parameters and how to use them in the Mapbox API Documentation’s [Tilequery section](https://docs.mapbox.com/api/maps/#tilequery).

### Access token

The only required item left is your access token, which you will find on your [Mapbox account page](https://account.mapbox.com/). The access token is required to track the requests you make from your account.

### Review the response

When you put it all together, your request will look like:

```
https://api.mapbox.com/v4/examples.4ze9z6tv/tilequery/-77.033835,38.89975.json?access_token={{ <UserAccessToken /> }}
```

Now that you have a request, take a look at what you get in return by pasting the full URL into a new browser window. Make sure that `access_token=` is set equal to your access token.

When you make your request, a JSON object is returned that contains, along with other information, a `TZID` property. This property shows the timezone of our test coordinates, the *America/New_York* timezone.

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.033835,
          38.89975
        ]
      },
      "properties": {
        "TZID": "America/New_York",
        "tilequery": {
          "distance": 0,
          "geometry": "polygon",
          "layer": "tz_world-c5z4hv"
        }
      }
    }
  ]
}
```

Now that you understand how Mapbox Tilequery API requests and responses both work, you can use this API request to build out your app’s functionality.

## Add the API request to the app

All modern browsers support the [HTML geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/Using_geolocation), which allows a browser to determine a user’s location if the user provides permission for it to do so. The timezone finder app will use the HTML geolocation API to get the longitude and latitude that will be used in the Mapbox Tilequery API call.

First, add the following code to your file above the closing `</body>` tag. This creates a place for you to add the JavaScript the app needs. The `accessToken` variable stores the access token that will be used in the query. Add your own access token between the quotation marks.

```html
<script>
  var accessToken = '{{ <UserAccessToken /> }}'; // add your access token here
</script>
```

Next, you will write a call to the HTML geolocation API to get the user's longitude and latitude. Add the following code after the `accessToken` variable you created:

```js
navigator.geolocation.getCurrentPosition(function(position) {
  var lon = position.coords.longitude;
  var lat = position.coords.latitude;
  console.log('Your location: ' + lon + ',' + lat);
});
```

Save your work and open this page in your browser. The browser will ask your permission to know your location. The `console.log` line will print the variables `lon` and `lat` to your browser’s console so that you can see the data that the HTML geolocation service returns.

Now it’s time to use this information to construct a Tilequery API call!

### Include Tilequery API

To use the Tilequery API, you will write a function called `getUserLocation` that will make a call to the API. This code will replace the call to the HTML geolocation API that you wrote in the last step, so erase that and replace it with the following code. Now the code between your opening and closing `script` tags should be:

```js
var accessToken = '{{ <UserAccessToken /> }}'; // add your access token here

function getUserLocation() {
  function success(position) {
    // create variables that will hold the
    // user's latitude and longitude data
    var lon = position.coords.longitude;
    var lat = position.coords.latitude;
    // construct a query to Tilequery API using the
    // longitude and latitude variables as parameters
    var query = 'https://api.mapbox.com/v4/examples.4ze9z6tv/tilequery/' + lon + ',' + lat + '.json?access_token=' + accessToken;

    // make the call to Tilequery API and parse the results
    $.ajax({
      method: 'GET',
      url: query,
    }).done(function(data) {
      // get the timezone from the resulting GeoJSON FeatureCollection
      var userTimezone = data.features[0].properties.TZID;
    });
  }
  // pass the results of a successful Tilequery API call
  // to the HTML geolocation API
  navigator.geolocation.getCurrentPosition(success);
}
```

### Add interactivity

Now you’re ready to add interactivity to your app! Add an event listener that calls the `getUserLocation` function when the user clicks the button.

To access the button, you can use its id `tz-button`. Create a new variable in your JavaScript right below the `accessToken` variable:

```js
var tzButton = document.getElementById('tz-button');
```

Now add an `onclick` event listener that will trigger the `getUserLocation` function when the button is clicked. Add the following line to your JavaScript below the `tzButton` variable declaration:

```js
tzButton.onclick = getUserLocation;
```

The code between your opening and closing `script` tags should now be:

```js
var accessToken = '{{ <UserAccessToken /> }}'; // add your access token here

// create a variable that selects the button
var tzButton = document.getElementById('tz-button');
// when the button is clicked, call the getUserLocation function
tzButton.onclick = getUserLocation;

function getUserLocation() {
  function success(position) {
    var lon = position.coords.longitude;
    var lat = position.coords.latitude;
    var query = 'https://api.mapbox.com/v4/examples.4ze9z6tv/tilequery/' + lon + ',' + lat + '.json?access_token=' + accessToken;

    $.ajax({
      method: 'GET',
      url: query,
    }).done(function(data) {
      var userTimezone = data.features[0].properties.TZID;
    });
  }

  navigator.geolocation.getCurrentPosition(success);
}
```

### Display messages

The only thing left to do is display the user’s timezone to the page! In the HTML section of your app, you already created a `div` that contains `p` tags with the ids `loading-message` and `return-message`. These will be used to display the success, error, and loading messages for your app. In the `getUserLocation` function, create variables for these elements:

```js
var loadingMessage = document.getElementById('loading-message');
var returnMessage = document.getElementById('return-message');
```

Now that you have selected these elements, you can start adding messages to them. Add a loading message at the beginning of the `getUserLocation` function that lets users know that the app is working on returning their information.

```js
document.getElementById('loading-message').textContent = 'loading';
```

The message will stand out since you already added an Assembly animation class to the `p` tag!

Now that you have a loading message, you need to remove the loading message add a success message. Since a success message is there to tell users when things have gone correctly, your app will display a message that tells users which area code they are in. First, though, you will need to remove the loading message. Add these lines to your JavaScript right below the `userTimezone` variable:

```js
loadingMessage.parentNode.removeChild(loadingMessage);
returnMessage.textContent = 'You are in the ' + userTimezone + ' timezone.';
```

There’s always the possibility for something to go wrong, and if that happens you need to let the user know. Add an error message near the end of the `getUserLocation` function:

```js
function error() {
  loadingMessage.parentNode.removeChild(loadingMessage);
  returnMessage.textContent = 'Sorry, unable to determine your current location.';
}
```

The code between your `script` tags will look like this now:

```js
var accessToken = '{{ <UserAccessToken /> }}'; // add your access token here

var loadingMessage = document.getElementById('loading-message');
var returnMessage = document.getElementById('return-message');

var tzButton = document.getElementById('tz-button');
tzButton.onclick = getUserLocation;

function getUserLocation() {
  // show a loading animation while we wait for the data
  document.getElementById('loading-message').textContent = 'loading';

  function success(position) {
    var lon = position.coords.longitude;
    var lat = position.coords.latitude;
    var query = 'https://api.mapbox.com/v4/examples.4ze9z6tv/tilequery/' + lon + ',' + lat + '.json?access_token=' + accessToken;

    $.ajax({
      method: 'GET',
      url: query,
    }).done(function(data) {
      var userTimezone = data.features[0].properties.TZID;
      // on success, remove the loading message and display the user's timezone
      loadingMessage.parentNode.removeChild(loadingMessage);
      returnMessage.textContent = 'You are in the ' + userTimezone + ' timezone.';
    });

  }

  // if anything goes wrong, remove the loading message and display an error message
  function error() {
    loadingMessage.parentNode.removeChild(loadingMessage);
    returnMessage.textContent = 'Sorry, unable to determine your current location.';
  }

  navigator.geolocation.getCurrentPosition(success, error);
}
```

## Finished product

You used the Mapbox Tilequery API to build an app that queries a custom tileset to determine a user’s timezone, without ever having to reference a rendered map. Open your app in the browser and try it out.

{{
  <DemoIframe gl={false} src="/help/demos/tilequery-intro/index.html" />
}}

## Next steps

To learn how to use cURL to upload large custom data sets like the one used in this tutorial to your Mapbox account, read the [Upload to Mapbox using cURL](/help/tutorials/upload-curl/) tutorial.
