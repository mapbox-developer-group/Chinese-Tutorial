---
title: Directions
description: Learn how Mapbox’s directions services work and how to add directions services to applications across platforms.
image: /img/narrative/directions.svg
topics:
  - directions
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import ChevronousText from '@mapbox/mr-ui/chevronous-text';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: guide
---

Mapbox provides a collection of APIs to add directions-related services to your application. Generate a route with trip durations, estimated distances, and turn-by-turn directions with the [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions), retrieve travel times between many points with the [Mapbox Matrix API](https://docs.mapbox.com/api/navigation/#matrix), retrieve duration-optimized trips between points with the [Mapbox Optimization API](https://docs.mapbox.com/api/navigation/#optimization), or align existing fuzzy routes to the routeable network with the [Mapbox Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching). From routing deliveries efficiently to providing navigation steps for wayfinding, Mapbox provides the tools necessary to integrate directions into your application.

This guide provides an overview of how the routing network is created, how to add directions services to applications across platforms, how to provide feedback, and relevant documentation to help you get started.

{{
  <DemoIframe src="/help/demos/how-mapbox-works/how-directions-works.html" />
}}

This example uses the [Mapbox GL Directions plugin](https://github.com/mapbox/mapbox-gl-directions) to add driving, cycling, or walking directions to a web application built with Mapbox GL JS. Type in two locations to view the raw JSON response for that query.

The Mapbox Directions API returns a JSON object containing a route with trip durations, estimated distances, and turn-by-turn instructions. When using the Mapbox GL Directions plugin, all this information will be automatically added to the map when a request is complete. By default, the plugin will also display turn-by-turn instructions. This example hides the turn-by-turn instructions and displays the raw JSON response to illustrate what information is included in the directions response object.

## How directions work

When you provide two or more points to the Mapbox Directions API, it returns a **route** as a GeoJSON line that you can add to your map, text for **turn-by-turn instructions** that you can choose to display in your application, and the **distance and estimated travel times** for the mode of transportation you selected. There are many other services that extend Mapbox directions that allow you to fix messy GPS traces to the network or optimize trips to multiple stops on a single journey.

### The routing network

A directions service that can create routes and optimized trips requires a robust network of paths with distinct attributes like speed, turn restrictions, and travel mode (for example, motorway, foot path, bike lane). Mapbox's directions services use a network of roads and paths, or *ways*, derived from [OpenStreetMap](http://learnosm.org/), a collaborative project to create a free and editable map of the world.

{{
  <Note
    title='Ways'
    imageComponent={<BookImage />}
  >
    <p>A <em>way</em> is an OpenStreetMap term used to describe an ordered list of nodes (points) which normally also has at least one tag, or description. For directions, ways can be roads, foot paths, or bicycle lanes.</p>
  </Note>
}}


Contributors to OpenStreetMap have built a vast, routeable network that includes properties like speed limits, turn lane restrictions, and accessibility for bikes and pedestrians. These details provide the framework that the [Open Source Routing Machine](http://project-osrm.org/) (OSRM) needs to calculate the most efficient path for your mode of transportation (driving, cycling, walking).

### Travel times

The Mapbox Directions API, Matrix API, and Optimization API all provide estimated trip durations. The time it takes to travel from one point to another is determined by many factors, including:

- The profile used (walking, cycling, or driving).
- The speed stored in the [`maxspeed` tag in OpenStreetMap](http://wiki.openstreetmap.org/wiki/Key:maxspeed).
- Traffic derived from real-time telemetry data (when the traffic profile is used).

### Traffic data

Incorporate real-time traffic into route selection and ETA generation using the `mapbox/driving-traffic` profile with the Mapbox [Directions API](https://docs.mapbox.com/api/navigation/#directions), [Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching), or [Matrix API](https://docs.mapbox.com/api/navigation/#matrix), or add a traffic layer to road geometries on a visual map. Read more about our traffic tileset in [Our map data](/help/how-mapbox-works/mapbox-data/#mapbox-traffic).


The `mapbox/driving-traffic` profile is available globally, but the accuracy of traffic-dependent travel times vary by country.

#### Highly accurate travel times

Traffic data collected in these countries is comprehensive across geographies and times, resulting in highly accurate travel times.

<div class="grid grid--gut24">
  <div class="col col--4">
     <ul>
       <li>Australia</li>
       <li>Canada</li>
       <li>Czech Republic</li>
       <li>Estonia</li>
       <li>Gibraltar</li>
       <li>Iceland</li>
     </ul>
  </div>
  <div class="col col--4">
     <ul>
       <li>Ireland</li>
       <li>Korea, Republic of</li>
       <li>Latvia</li>
       <li>Liechtenstein</li>
       <li>Netherlands</li>
     </ul>
  </div>
  <div class="col col--4">
     <ul>
       <li>New Zealand</li>
       <li>Puerto Rico</li>
       <li>Slovakia</li>
       <li>United Kingdom</li>
       <li>United States of America</li>
     </ul>
  </div>
</div>

#### Moderately accurate travel times

Traffic data collected in these countries is less comprehensive. Travel times may be inaccurate, especially in heavy and unusual traffic conditions.

<div class="grid grid--gut24">
  <div class="col col--4">
    <ul>
      <li>Andorra</li>
      <li>Argentina</li>
      <li>Armenia</li>
      <li>Austria</li>
      <li>Barbados</li>
      <li>Belarus</li>
      <li>Belgium</li>
      <li>Belize</li>
      <li>Cayman Islands</li>
      <li>Chile</li>
      <li>Cyprus</li>
      <li>Denmark</li>
      <li>Dominican Republic</li>
    </ul>
  </div>
  <div class="col col--4">
    <ul>
      <li>Finland</li>
      <li>France</li>
      <li>Germany</li>
      <li>Guam</li>
      <li>Hungary</li>
      <li>Iran, Islamic Republic of</li>
      <li>Israel</li>
      <li>Italy</li>
      <li>Japan</li>
      <li>Jordan</li>
      <li>Lithuania</li>
      <li>Luxembourg</li>
      <li>Mexico</li>
    </ul>
  </div>
  <div class="col col--4">
  <ul>
    <li>Montenegro</li>
    <li>Norway</li>
    <li>Panama</li>
    <li>Paraguay</li>
    <li>Poland</li>
    <li>Portugal</li>
    <li>Romania</li>
    <li>Slovenia</li>
    <li>Spain</li>
    <li>Sweden</li>
    <li>Switzerland</li>
    <li>United Arab Emirates</li>
    <li>Uruguay</li>
  </ul>
  </div>
</div>

#### Limited predictability of travel times

Traffic data collected in these countries is less comprehensive. Travel times are less reliable, with partial coverage of traffic conditions.

<div class="grid grid--gut24">
  <div class="col col--4">
    <ul>
      <li>Åland Islands</li>
      <li>Albania</li>
      <li>Algeria</li>
      <li>American Samoa</li>
      <li>Anguilla</li>
      <li>Aruba</li>
      <li>Azerbaijan</li>
      <li>Bahamas</li>
      <li>Bahrain</li>
      <li>Bangladesh</li>
      <li>Bermuda</li>
      <li>Bolivia, Plurinational State of</li>
      <li>Bosnia and Herzegovina</li>
      <li>Botswana</li>
      <li>Brazil</li>
      <li>Brunei Darussalam</li>
      <li>Bulgaria</li>
      <li>Cambodia</li>
      <li>Cameroon</li>
      <li>Colombia</li>
      <li>Cook Islands</li>
      <li>Costa Rica</li>
      <li>Côte d'Ivoire</li>
      <li>Croatia</li>
      <li>Dominica</li>
      <li>Ecuador</li>
      <li>Egypt</li>
      <li>El Salvador</li>
      <li>Faroe Islands</li>
      <li>Fiji</li>
      <li>French Polynesia</li>
      <li>Georgia</li>
      <li>Ghana</li>
    </ul>
  </div>
  <div class="col col--4">
    <ul>
      <li>Greece</li>
      <li>Grenada</li>
      <li>Guatemala</li>
      <li>Haiti</li>
      <li>Holy See (Vatican City State)</li>
      <li>Honduras</li>
      <li>Hong Kong</li>
      <li>India</li>
      <li>Indonesia</li>
      <li>Iraq</li>
      <li>Jamaica</li>
      <li>Kazakhstan</li>
      <li>Kenya</li>
      <li>Kuwait</li>
      <li>Kyrgyzstan</li>
      <li>Laos</li>
      <li>Lebanon</li>
      <li>Macedonia, the Former Yugoslav Republic of</li>
      <li>Malawi</li>
      <li>Malaysia</li>
      <li>Malta</li>
      <li>Mauritius</li>
      <li>Moldova, Republic of</li>
      <li>Monaco</li>
      <li>Mongolia</li>
      <li>Morocco</li>
      <li>Myanmar</li>
      <li>Namibia</li>
      <li>Nepal</li>
      <li>New Caledonia</li>
      <li>Nicaragua</li>
      <li>Nigeria</li>
    </ul>
  </div>
  <div class="col col--4">
    <ul>
      <li>Oman</li>
      <li>Pakistan</li>
      <li>Philippines</li>
      <li>Qatar</li>
      <li>Russian Federation</li>
      <li>Saint Barthélemy</li>
      <li>Saint Kitts and Nevis</li>
      <li>Saint Lucia</li>
      <li>Saint Martin (French part)</li>
      <li>San Marino</li>
      <li>Saudi Arabia</li>
      <li>Senegal</li>
      <li>Serbia</li>
      <li>Sierra Leone</li>
      <li>Singapore</li>
      <li>Sint Maarten (Dutch part)</li>
      <li>South Africa</li>
      <li>Sri Lanka</li>
      <li>Swaziland</li>
      <li>Tajikistan</li>
      <li>Tanzania, United Republic of</li>
      <li>Thailand</li>
      <li>Trinidad and Tobago</li>
      <li>Tunisia</li>
      <li>Turkey</li>
      <li>Turks and Caicos Islands</li>
      <li>Ukraine</li>
      <li>Uzbekistan</li>
      <li>Venezuela, Bolivarian Republic of</li>
      <li>Viet Nam</li>
      <li>Virgin Islands, British</li>
      <li>Zambia</li>
    </ul>
  </div>
</div>

## Using directions services

There are many tools you can use to enable directions-related services for your Mapbox web or mobile application. You can access these services directly using the web services APIs, through our Navigation SDK, or using one of several plugins and libraries to integrate these services into applications across platforms.

### Web services APIs

There are four directions-related services that Mapbox offers:

- **Mapbox Directions API**: retrieve point to point directions including a route with durations, estimated distances, and turn-by-turn instructions.
- **Mapbox Matrix API**: retrieve all travel times between many points.
- **Mapbox Optimization API**: retrieve duration-optimized trips between input coordinates.
- **Mapbox Map Matching API**: align existing fuzzy routes to the routeable network.

Read more about the required inputs for each API below.


#### Mapbox Directions API

Requesting directions from the [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) requires at least two waypoints &mdash; an origin and a destination &mdash; but can also include up to 23 additional waypoints between (or a total of 25 waypoints). When making a request, you can specify additional parameters such as which **profile** to use (walking, cycling, driving, or driving with traffic) and whether alternate routes should be included in the response. You can also add optional annotations to your request, including duration, distance, speed, and congestion. We calculate congestion by comparing night-time traffic speeds with real-time traffic speeds and assign a level of congestion given the percentage difference.

You can read more about the directions response object in our [API documentation](https://docs.mapbox.com/api/navigation/#directions-response-object).

{{
  <DemoIframe src="https://www.mapbox.com/bites/00321/#14.48/38.9101/-77.0373" />
}}


#### Mapbox Matrix API

The Mapbox Matrix API returns travel times between many locations. Each location is either a source or destination. The number of sources and destinations are multiplied to create the matrix, or timetable, and calculate the number of [elements](/help/glossary/matrix-api-elements/) needed to make the request. For example, given three locations A, B, C, the Matrix API will return a matrix of all travel times in **seconds** between all locations:

|   | A     | B     | C     |
| - | ----- | ----- | ----- |
| A | A → A | A → B | A → C |
| B | B → A | B → B | B → C |
| C | C → A | C → B | C → C |

The Matrix API will always return the duration on the most efficient route for each location in the matrix, where an element is an origin-destination pair in the matrix.

Durations between locations may not be symmetric (for example A to B may have a different duration than B to A), as the routes may differ by direction due to one-way streets or turn restrictions. The Matrix API returns durations in seconds. It does not return route geometries or distances. Like the [Directions API](https://docs.mapbox.com/api/navigation/#directions), the Matrix API must be used on the same continent (does not cross over water bodies).

This API allows you to build tools that efficiently check the reachability of coordinates from each other, filter locations by travel time, or run your own algorithms for solving optimization problems.

Each request requires that you specify which locations are the **sources** and which are the **destinations**. There are four types of requests you can use with the Matrix API:

<div class='grid grid--gut24 mt24'>
  <div class='col col--7-ml col--12'>
    <p><strong>Many to many (NxN)</strong></p>

    <p>A many to many request is the default and generates the most results per-number-of-coordinates. This assumes all locations are sources and destinations. Without passing the source and destinations in the request, the response will still output an array of travel times between all locations.</p>

    <pre><code>
    https://api.mapbox.com/directions-matrix/v1/mapbox/driving/A;B;C;D;E?access_token=....
    </code></pre>
  </div>
  <div class='col col--5-ml col--12'>
    <img alt="Many to Many (NxN)" src="/help/img/directions/matrix-nxn.png" />
  </div>
</div>

<div class='grid grid--gut24 mt24'>
  <div class='col col--7-ml col--12'>
    <p><strong>One to many (1xN)</strong></p>

    <p>In some cases, you may have a single source (for example, one driver) and four potential destinations (four gas stations). To calculate which destination has the shortest drive time, you need to specify the source and destination coordinates.</p>

    <pre><code>
    https://api.mapbox.com/directions-matrix/v1/mapbox/driving/A;B;C;D;E?sources=0&destinations=1;2;3;4&access_token=...
    </code></pre>
  </div>
  <div class='col col--5-ml col--12'>
    <img alt="One to many (1xN)" src="/help/img/directions/matrix-1xn.png" />
  </div>
</div>

<div class='grid grid--gut24 mt24'>
  <div class='col col--7-ml col--12'>
    <p><strong>Many to one (Nx1)</strong></p>

    <p>An opposite request may be necessary where you may want to find travel times of many taxis to one rider, for example. In this case, a many to one (Nx1) request can be made by listing all your sources and your one destination.</p>

    <pre><code>
    https://api.mapbox.com/directions-matrix/v1/mapbox/driving/A;B;C;D;E?sources=1;2;3;4&destinations=0&access_token=....
    </code></pre>
  </div>
  <div class='col col--5-ml col--12'>
    <img alt="Many to one (Nx1)" src="/help/img/directions/matrix-nx1.png" />
  </div>
</div>

<div class='grid grid--gut24 mt24' markdown='1'>
  <div class='col col--7-ml col--12' markdown='1'>
    <p><strong>Several to several (MxN)</strong></p>

    <p>An uncommon but useful case is a several to several (NxM) request where you may want to be selective about how many sources and destinations you wish to find travel times to and from.</p>

    <pre><code>
    https://api.mapbox.com/directions-matrix/v1/mapbox/driving/A;B;C;D;E?sources=0;1&destinations=2;3;4&access_token=....
    </code></pre>
  </div>
  <div class='col col--5-ml col--12'>
    <img alt="Several to several NxM" src="/help/img/directions/matrix-nxm.png" />
  </div>
</div>

#### Mapbox Optimization API

The [Mapbox Optimization API](https://docs.mapbox.com/api/navigation/#optimization) returns a duration-optimized trip between the input coordinates. This is also known as solving the [Traveling Salesperson Problem](https://en.wikipedia.org/wiki/Travelling_salesman_problem). This API could be used to plan a route for deliveries in a city. Optimized trips can be retrieved for  driving, bicycling, and walking or hiking.

![optimized trips](/help/img/directions/routing.gif)


#### Mapbox Map Matching API

The [Mapbox Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching) snaps fuzzy, inaccurate traces from a GPS unit or a phone to the OpenStreetMap road and path network using the Directions API. This produces clean paths that can be displayed on a map or used for other analysis.

![map matching](https://i.imgur.com/j32cq1x.gif)

### Mapbox Navigation SDK

You can add directions to a mobile application using the [Mapbox Navigation SDK for iOS and Android](https://www.mapbox.com/navigation-sdk/). With the Navigation SDK, it takes only a few lines of code to display a complete navigation experience inside your app. With the Navigation SDK, you can:

- Generate turn-by-turn instructions.
- Use automatic rerouting when a user deviates from the route.
- Provide walking, biking, and driving directions.
- Provide real-time traffic.

![navigation SDK](/help/img/directions/nav.png)

Read more about the Navigation SDK for [iOS](https://www.mapbox.com/ios-sdk/navigation/) and [Android](https://www.mapbox.com/android-docs/navigation/).

### Libraries and plugins

We have several tools across platforms that allow you to integrate the Mapbox Directions API into your existing applications seamlessly:

- **Web**: [Mapbox GL Directions plugin](https://www.mapbox.com/mapbox-gl-js/example/mapbox-gl-directions/) for Mapbox GL JS and [Mapbox-directions.js](https://www.mapbox.com/mapbox.js/plugins/) for Mapbox.js
- **Android**: [Mapbox Java SDK](https://www.mapbox.com/android-docs/java-sdk/examples/#directions)
- **iOS**: [MapboxDirections.swift](https://github.com/mapbox/MapboxDirections.swift)

These tools allow you to add routing capabilities to your application, but have limitations when it comes to customization. These tools do not provide access to the Mapbox Matrix API, Optimization API, or Map Matching API. For more flexibility, you can [use our APIs directly](#web-services-apis).

In addition, we offer libraries for:

- [Python](https://github.com/mapbox/mapbox-sdk-py)
- [JavaScript](https://github.com/mapbox/mapbox-sdk-js)

Here's an example of the [Mapbox GL Directions plugin](https://www.mapbox.com/mapbox-gl-js/example/mapbox-gl-directions/) in action:

![Mapbox GL JS plugin](/help/img/directions/gljs-plugin.png)

### Testing the API

If you would like to get a feel for how the Mapbox Directions API works without building a whole application, we also provide an [API Playground](https://www.mapbox.com/api-playground/#/directions). Besides providing a convenient user interface to test queries, the API playground allows you to test the API's URL and query parameters, such as mode of transportation, steps, and alternative routes.

<a class='txt-bold' href='https://www.mapbox.com/api-playground/#/directions'>{{<ChevronousText text="Visit the API Playground" />}}</a>


## Providing directions feedback

If you find issues with routing or any of the related services, you can provide feedback on our [Directions Feedback page](https://www.mapbox.com/feedback/). If you are using the API directly, you can use the [API Playground](https://www.mapbox.com/api-playground/#/directions?_k=8qemr9) to test your request, response, and any parameters you would like to include in your request.
