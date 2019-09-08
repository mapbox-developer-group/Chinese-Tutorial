---
标题：在iOS系统上搭建商铺定位
概述：搭建可以内置在iOS系统应用的商铺定位
缩略：ios商铺定位
级别：3
主题:
- 移动应用
编程语言:
- Swift
- Objective-C
prereq: Familiarity with Xcode, Swift, and CocoaPods.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: tutorial
---

This guide will walk you through how to use our **iOS Store Locator starter kit** to create a custom store locator map that can be integrated into any iOS application. You'll be able to browse several locations, select a specific location to view more information, and retrieve a route from a user's location to any of the store locations. You can start with one of five different themes and customize everything from store location data to marker icons and individual store cards.

{{<img alt='animated GIF of a store locator application on an iOS device' src='/help/img/ios/store-locator-final-product.gif' className='wmax360 block mx-auto' />}}

## Getting started

The iOS Store Locator starter kit runs on iOS 9.0 and above. It can be used with code written in Swift 3.1 and above using Xcode 9. Here are the resources you’ll need before getting started:

- **Starter kit files**. Download or clone the [iOS Store Locator starter kit](https://github.com/mapbox/store-locator-ios/) from GitHub. This includes all the necessary files for a functional Xcode project.
- **A Mapbox account and access token**. Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account/). You will add your access token to your Info.plist file.
- **A physical or [simulated iOS device](https://help.apple.com/simulator/mac/current/#/deve44b57b2a)**.
- **Optional: SVG editing tool**. If you'd like to create custom icons, you can use a program like [Sketch](http://sketchapp.com), [Figma](http://figma.com), or Adobe Illustrator.


## Set up the starter kit

The [iOS Store Locator starter kit](https://github.com/mapbox/store-locator-ios/) includes all the source files needed to build a store locator. The kit includes:

- Five UI theme variations.
- Sample GeoJSON data with store locations.
- Code for retrieving directions with the [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) and displaying a navigation route line on the map.

### Install dependencies

Start by installing the project's dependencies using CocoaPods. If you're new to CocoaPods, read the [CocoaPods documentation](https://guides.cocoapods.org/using/getting-started.html) before getting started. You'll need to run `pod update` in the directory containing the starter kit files to add the necessary pods (**Mapbox-iOS-SDK** and **MapboxDirections.swift**) to your project.

Once you’ve run `pod update`, work out of the space `mapbox-store-locator.xcworkspace` (not `mapbox-store-locator.xcodeproj`). The `mapbox-store-locator.xcworkspace` includes the necessary dependencies. The easiest way to do this from the command line is to use `open mapbox-store-locator.xcworkspace/` after your pods have been installed.

### Add access token

As soon as you open your project in Xcode 9, you'll need to add your access token to the `Info.plist` file to display a map. You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account/). To add your access token to the project:

1. Open `Info.plist`.
1. Find the `MGLMapboxAccessToken` _Key_ and replace the placeholder _Value_, `<Add Access Token>`, with your access token.

### `ThemeViewController`

The `ThemeViewController.swift` file is the primary place where you’ll customize your code. Within the `ThemeViewController.swift` file, you can:

- Select a theme.
- Set the map's style URL.
- Choose the marker icons.
- Customize other UI elements and colors as needed.

{{
    <Note
      imageComponent={<BookImage />}
    >
        <p>The starter kit files include detailed inline comments that tell you what customizations are possible.</p>
    </Note>
}}

## Choose a theme

Once you have the starter kit set up, start customizing your application by picking a theme.

### Explore themes

Unless adjusted, the theme picker preview will be the first thing you see when the app is launched. Run your application and browse available themes by clicking on the preview image for one of five themes made by our mobile designers.

{{<img alt='animated GIF of a user clicking through to preview various available themes' src='/help/img/ios/store-locator-explore-themes.gif' className='wmax360 block mx-auto' />}}

### Set the theme

In this tutorial you'll work with the fifth theme displayed in the theme picker preview, the `neutralTheme`. This theme features the [Mapbox Streets](https://www.mapbox.com/maps/streets/) style and a house icon at each store location. To set this theme:

1. Open the `ThemeViewController.swift` file.
1. Find the line `var viewControllerTheme : Theme?` and delete it.
1. Then find the line `// var viewControllerTheme : Theme? = MBXTheme.purpleTheme`, which has been commented out.
1. Highlight the line and use `command` + `/` to uncomment the line.
1. Replace `.purpleTheme` with `.neutralTheme`.

Now you've chosen the neutral theme, but your application is still set up to start with the theme picker preview when it is initialized. Next, you'll change the initial view controller.

### Change the initial view controller

1. Open `Main.storyboard`.
1. Click on **Theme View Controller Scene**.
1. Click on the Attributes inspector in the upper right side.
1. Check the box next to *Is Initial View Controller*.

![screenshot of how to set the initial view controller in Xcode](/help/img/ios/store-locator-set-initial-view.png)

Run your application, and it will display a map using the Mapbox Streets style with several house icons.

{{<img alt='screenshot of a map with several markers on an iOS device using the neutral theme centered on New York City' src='/help/img/ios/store-locator-choose-a-theme.png' className='wmax360 block mx-auto' />}}

## Add your data

The starter kit contains a GeoJSON file called `stores.geojson`  where you’ll find all the current store locations that are visible on the map. [GeoJSON](/help/glossary/geojson/) is a file format for geospatial data and a subset of the JSON format. In this section, you'll update the sample data to reflect your actual store locations.

Locate the `stores.geojson` file and take a look at how the data is formatted. Notice that each store location is a separate GeoJSON _feature_ in the file. Each feature has four `properties` describing a few characteristics about the store location and `geometry` specifying that the feature is a single point and where that point is located in the world.

If you have store location data available in GeoJSON form, you can delete the current data and replace it with your own.

### Replace data

In this guide, we've provided GeoJSON data for you to use in this step. In this example, you'll replace the current GeoJSON data in `stores.geojson` with [animal shelters in Cook County, Illinois](https://datacatalog.cookcountyil.gov/dataset/Area-Animal-Shelters-Map/t86e-hv9w). Then, you'll adjust the bounding box and mock user location and run your app to see the new store locations.


```json
{
  "features": [
    {
      "type": "Feature",
      "properties": {
        "description": "18736 W Peterson Rd, Libertyville",
        "name": "Lake County Animal Care and Control",
        "hours": "M-F 9am-4:30pm, Sat 9am-12:30pm",
        "phone": "847-377-4700"
      },
      "geometry": {
        "coordinates": [
          -87.998316,
          42.306035
        ],
        "type": "Point"
      },
      "id": "address.10164434706493830"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1103 W End Ave N, Chicago Heights",
        "name": "Animal Care League",
        "hours": "M-F 9am-5pm",
        "phone": "708-848-8155"
      },
      "geometry": {
        "coordinates": [
          -87.79962,
          41.872075
        ],
        "type": "Point"
      },
      "id": "address.11842842831717040"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1375 N Roselle Rd, Schaumburg",
        "name": "Golf Rose Animal Hospital",
        "hours": "M-F 8am-7pm, Sat 9am-2pm",
        "phone": "847-885-3344"
      },
      "geometry": {
        "coordinates": [
          -88.079033,
          42.053136
        ],
        "type": "Point"
      },
      "id": "address.14288456127471660"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1634 S Laramie Ave, Cicero",
        "name": "Waggin Tails",
        "hours": "M-F 1pm-6pm",
        "phone": "708-652-0825"
      },
      "geometry": {
        "coordinates": [
          -87.755487,
          41.85705
        ],
        "type": "Point"
      },
      "id": "address.14994575158876850"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "5127 Oakton St, Skokie",
        "name": "Skokie Animal Control",
        "hours": "not available",
        "phone": "847-933-8484"
      },
      "geometry": {
        "coordinates": [
          -87.71049,
          42.024031
        ],
        "type": "Point"
      },
      "id": "address.15065751370530970"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "10305 Southwest Hwy, Chicago Ridge",
        "name": "Animal Welfare League (AWL)",
        "hours": "M-Sat 9am-9pm, Sun 9am-6pm",
        "phone": "708-636-8586"
      },
      "geometry": {
        "coordinates": [
          -87.787701,
          41.703627
        ],
        "type": "Point"
      },
      "id": "address.17674198339620830"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1103 W End Ave N, Chicago Heights",
        "name": "Paws Tinley Park",
        "hours": "M, W, F 7pm-9pm, T, Th, Sat, Sun 12pm-4pm",
        "phone": "815-464-7298"
      },
      "geometry": {
        "coordinates": [
          -87.806946,
          41.543834
        ],
        "type": "Point"
      },
      "id": "address.5098323152873800"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1103 W End Ave N, Chicago Heights",
        "name": "South Suburban Humane Society",
        "hours": "M, W, F 1pm-7pm, Sat-Sun 12pm-5pm",
        "phone": "708-755-7387"
      },
      "geometry": {
        "coordinates": [
          -87.631074,
          41.511524
        ],
        "type": "Point"
      },
      "id": "address.6529417923998300"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1634 S Laramie Ave, Cicero",
        "name": "DuPage County Animal Hospital",
        "hours": "M, Th 8am-7:30pm, T, W, F 8am-5pm, Sat 10am-3pm",
        "phone": "630-407-2800"
      },
      "geometry": {
        "coordinates": [
          -88.143366,
          41.866063
        ],
        "type": "Point"
      },
      "id": "address.7211235368236180"
    },
    {
      "type": "Feature",
      "properties": {
        "description": "1375 N Roselle Rd, Schaumburg",
        "name": "Evanston Animal Shelter & Animal Control",
        "hours": "M-F 8am-7pm, Sat 9am-2pm",
        "phone": "847-866-5082"
      },
      "geometry": {
        "coordinates": [
          -87.6712,
          42.0267
        ],
        "type": "Point"
      },
      "id": "neighborhood.281624"
    }
  ],
  "type": "FeatureCollection"
}
```

Replace the data in the `stores.geojson` file to reflect your actual store locations. Open the `stores.geojson` file. Delete the current contents and add the GeoJSON data above. The data that's provided in the sample code and in this example contain four properties for each store location:

- `name`
- `description`
- `hours`
- `phone`

Since all the feature `properties` are identical to the four that were used in the initial GeoJSON data, your map will be fully functional immediately. If you have different information you would like to display as `properties`, you will need to update the related code in the `ThemeViewController.swift` file &mdash; look for the code immediately following the `// MARK: Update the attribute keys based on your data's format` comment.

{{
    <Note
      title='Create a GeoJSON file from scratch'
      imageComponent={<BookImage />}
    >
      <p>There are several ways to create GeoJSON data. If you don't have GeoJSON data containing store information, you can use the <a href='https://www.mapbox.com/studio-manual/reference/datasets/#dataset-editor'>Mapbox Studio dataset editor</a>, a convenient in-browser application for creating and editing Mapbox <a href='/help/glossary/dataset/'>datasets</a>.</p>
      <p>First, create a new dataset:</p>
      <ol>
          <li>Log into Mapbox Studio and navigate to the <a href='https://www.mapbox.com/studio/datasets'>Datasets page</a>.</li>
          <li>Click the <strong>New dataset</strong> button.</li>
          <li>A new window will open. You'll use the <strong>Blank dataset</strong> option in the upper right corner.</li>
          <li>Name your dataset and click <strong>Create</strong>.</li>
          <li>The dataset editor will automatically open.</li>
      </ol>
      <p>Next, begin adding stores. You can use the geocoder in the dataset editor to search for a place and the draw tools to add a new point to your dataset. You can change the geometry, placement, and properties of existing features with the dataset editor’s draw tools.</p>
      <p>After you've added each location, you can <strong>Save</strong>, return to the <a href='https://www.mapbox.com/studio/datasets'>Datasets page</a>, click the <strong>Menu</strong><Icon name="menu" inline={true} /> button next to the name of your dataset, and click <strong>Download</strong> to retrieve GeoJSON.</p>
    </Note>
}}

## Simulate user location and center map

The `ThemeViewController.swift` file specifies that the map be centered on New York when the app is initialized. Next, you'll update the user's simulated location to Cook County in Illinois.

### Allow user location

Before you can draw a user’s location on the map, you must ask for their permission and give a brief explanation of how your application will use their location data. By default, location permissions are already configured in the starter kit files.

You can edit the location usage description by setting the `NSLocationWhenInUseUsageDescription` key in the Info.plist file. We recommend setting the value to the following string, which is the application's location usage description: `Shows your location on the map and helps improve OpenStreetMap`. iOS 11 requires that you provide a `NSLocationAlwaysAndWhenInUseUsageDescription` in addition to a `NSLocationWhenInUseUsageDescription`. We recommend providing a different string for this key to help your users decide which level of permission they wish to grant to your application. When a user opens your application for the first time, they will be presented with an alert that asks them if they would like to allow your application to access their location.

### Simulate user location

When you run your app in Simulator, you’ll be presented with a dialog box asking for permission to use Location Services. Click **Allow**. You won’t see your location on the map until you go to Simulator’s menu bar and select **Debug > Location > Custom Location**. Enter `41.948` for latitude, `-87.839` for longitude, and you'll see the location dot appear in the middle of Cook County.

{{
    <Note
      title='Simulating user location on a physical device'
      imageComponent={<BookImage />}
    >
        <p>If you are running your application on a physical device instead of on Simulator, you will need to create a GPX file containing the coordinates (<code>41.948</code> for latitude, <code>-87.839</code> for longitude). Name your file <code>Chicago</code>. Then, use <strong>Product > Scheme > Edit Scheme</strong> to change <em>Default location</em> to <code>Chicago</code>.</p>
    </Note>
}}

Finally, adjust the zoom level of the mapView. Within the `viewDidLoad` function, find `mapView.zoomLevel` and set it equal to `8`.

```swift
override func viewDidLoad() {
    ...

    mapView.zoomLevel = 8

    ...
}
```

Once you’ve updated the user location information, the Mapbox Directions API will automatically read your GeoJSON file to retrieve routes to each of your locations.

Run your application and you will see a map centered on Cook County displaying your new data.

{{<img alt='screenshot of a map with several markers on an iOS device using the neutral theme centered on Cook County Illinois' src='/help/img/ios/store-locator-add-data.png' className='wmax360 block mx-auto' />}}

## Add custom markers

Your application uses house icon to show the location of each animal shelter, but with the store locator kit you can customize icons to be whatever you'd like. Next, you'll switch to the current house icon to a dog icon.

{{<img alt='preview of a selected dog icon' src='/help/img/ios/store-locator-dog-icon-selected.png' className='wmax120 mx-auto block' />}}

### Add the icon as an asset

The images used for the icons are located in the `Assets.xcassets` folder. Open the folder and browse the current files. You'll see that there are two house icons: `blue_selected_house` and `blue_unselected_house`. Right-click on `blue_selected_house` and click **Show in finder**.

You'll see that each icon comes from a folder, in this case `blue_selected_house.imageset`. Inside that folder are two files: a PDF of the image and a [`Contents.json` file](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_ref-Asset_Catalog_Format/ImageSetType.html).

Upload two new dog icons (one for when the icon is selected and one when it is not selected):

1. Download [this zipped file](/help/demos/ios-store-locator/dog_icon.zip) that contains an image set for two dog icons.
1. Unzip and add the contents to the `Assets.xcassets` folder in your project.

### Change icon references

Next, you need to change all references to the house icons to point to the dog icons instead. In the `Themes.swift` file, find references to `blue_selected_house` and `blue_unselected_house` and replace with `blue_selected_dog` and `blue_unselected_dog` respectively.

```swift
static let neutralTheme = Theme(defaultMarker: UIImage(named: "blue_unselected_dog")!,
    selectedMarker: UIImage(named: "blue_selected_dog")!,
    styleURL: MGLStyle.streetsStyleURL,
    themeColor: ThemeColor.neutralTheme,
    fileURL: Bundle.main.url(forResource: "stores", withExtension: "geojson")!)
```

Run your application, and you will see a map with dog icons at the location for each animal shelter.

{{<img alt='screenshot of a map with several markers with dog icons on an iOS device' src='/help/img/ios/store-locator-custom-markers.png' className='wmax360 block mx-auto' />}}

## Customize cards

Besides customizing the map and icons, you can also customize the design of the cards that display information about a location when it is clicked. Next, you'll customize the background color of the top half of the cards. In the `Themes.swift` file, replace the current `primaryDarkColor` for the `neutralTheme` from gray to blue:

```swift
static let neutralTheme = Color(primaryColor: UIColor(red:0.91, green:0.90, blue:0.88, alpha:1.0),
    // The line below has been updated from gray to blue
    primaryDarkColor: UIColor(red: 0.2706, green: 0.6667, blue: 0.9098, alpha: 1.0),
    navigationLineColor: UIColor(red:0.00, green:0.73, blue:1.00, alpha:1.0),
    lowerCardTextColor: UIColor.black,
    accentColor: UIColor.white)
```

Run your application, click on a location, and you will see an updated card with a blue background.

{{
<div className='my12 grid grid--gut12'>
  <div className='col col--6-mm col--12 align-center'>
    <img alt='screenshot of an iOS device with a map with a marker selected displaying an information card with a gray background' src='/help/img/ios/store-locator-custom-card-before.png' className='hmax360' />
    <div><em>Before customizing</em></div>
  </div>
  <div className='col col--6-mm col--12 align-center'>
    <img alt='screenshot of an iOS device with a map with a marker selected displaying an information card with a blue background' className='hmax360' src='/help/img/ios/store-locator-custom-card-after.png' />
    <div><em>After customizing</em></div>
  </div>
</div>
}}

## Final product

You've learned how the iOS Store Locator starter kit works and modified a few of the key customizable elements of a store locator.

{{<img alt='animated GIF of a store locator application on an iOS device' src='/help/img/ios/store-locator-final-product.gif' className='wmax360 block mx-auto' />}}

## Next steps

Take a look at the [Mapbox Maps SDK for iOS documentation](https://www.mapbox.com/ios-sdk/) and [examples](https://www.mapbox.com/ios-sdk/examples) to learn more about customizing your application or adding additional functionality. If you're interested in creating your own custom map style to replace the designer themes provided in the iOS Store locator starter kit, complete our [Create a custom style](/help/tutorials/create-a-custom-style/) tutorial to use Mapbox Studio to build a style that fits your brand.
