---
title: Custom map styles in Unity
description: Use a custom map style from Mapbox Studio in a Unity application.
thumbnail: unityCustomStyle
level: 2
topics:
- unity
language:
- No code
prereq: Familiarity with Unity.
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
contentType: tutorial
---

Mapbox allows you to create completely custom maps that can be used across platforms. This tutorial will walk you through how to add a [Mapbox designer map](https://www.mapbox.com/designer-maps/) to your account as a custom style and use that custom style with the Mapbox Maps SDK for Unity.

![A map of San Francisco using the custom Whaam! style](/help/img/unity/unity-custom-style-final-product.png)

## Getting started

Here are some resources you'll need to get started:

- **Mapbox account and access token.** Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account/).
- **A Unity scene including the Mapbox Maps SDK for Unity.** You can follow our tutorial, [Mesh generation with the Maps SDK for Unity Part 1](/help/tutorials/unity-mesh-pt-1/), to add a map to a scene in Unity.
- **Style URL.** You will use the [style URL](/help/glossary/style-url/) associated with your custom style to add the style to your Unity project.

## Learn about map styles

A map [style](/help/glossary/style/) is a document that defines the visual appearance of a map. The style document states which data sources to use and creates style layers that specify how that data should be styled. With the Mapbox Maps SDK for Unity, you can use one of our core Mapbox styles (like Mapbox Streets, Mapbox Outdoors, and Mapbox Satellite) or a custom map style from your Mapbox account.

You can create a custom style in the Mapbox Studio style editor. For more information on creating custom styles, explore the following resources:

- Our [Create a custom style](/help/tutorials/create-a-custom-style/) tutorial.
- The [Styles section of the Mapbox Studio manual](https://www.mapbox.com/studio-manual/reference/styles/).
- Our [Map design](/help/how-mapbox-works/map-design/) guide.

You can also add one of our designer map styles to your account and use it in your Unity application. In this tutorial, you'll use the designer map style, [Whaam!](https://www.mapbox.com/designer-maps/#whaam)

{{<a href='https://www.mapbox.com/designer-maps/' className='txt-bold'>Browse all designer maps and add them to your account <Icon name='arrow-right' inline={true} /></a>}}

![a preview of all designer map styles](/help/img/studio/designer-maps.png)

## Add a designer style to your account

Start by signing into your Mapbox account. Once you are signed in, visit the designer map page to add a new style to your account:

1. Visit [mapbox.com/designer-maps](https://www.mapbox.com/designer-maps/).
1. Find the _Whaam!_ style and click **Add this style**.
1. The style will automatically be added to your Mapbox account.

When the style is added to your account, it will appear on the [Styles page in Mapbox Studio](https://www.mapbox.com/studio/styles). From here, you can find the [style URL](/help/glossary/style-url) for the style. You'll use the style URL to add this style to your Unity application:

1. Find the style on your Styles page.
1. Click on the **Menu {{<Icon name='menu' inline={true} />}}** next to the style name to uncover options for altering and using that style.
1. Find the _Style URL_. You can use the {{<Icon name='clipboard' inline={true} />}} clipboard icon to copy the style URL, which you'll paste into your Unity project in a later step.


## Add a custom style in Unity

Next, you'll add this style in Unity using the style URL.

### Set up a map in Unity

First, you'll need to set up a new scene displaying a map. You can follow our tutorial for [how to add a map in Unity](/help/tutorials/create-a-map-in-unity/). After completing the tutorial, you should see a map using a default Mapbox style within the Unity interface.


![A map of San Francisco using the built in Dark theme](/help/img/unity/unity-custom-style-starting-map.png)


### Change the map style in Unity

Next, change the style of the map. In Unity, open the inspector window of your Map object. Look for the IMAGES section of the `Abstract Map` component. Change the *Style Name* to **Custom**. Copy and paste the [style URL](/help/glossary/style-url/) from the [Mapbox Studio Styles page](https://www.mapbox.com/studio/styles) into the *Map Id* field.

<p><img src="/help/img/unity/unity-custom-style.png" alt="Custom Map ID field" /></p>

## Final product

When you run your scene with the new style, you'll see how your map has changed.

![A map of San Francisco using the custom Whaam! style](/help/img/unity/unity-custom-style-final-product.png)


## Next steps

There are many other ways for you to customize your Unity application. Explore the following resources to continue building your application:

- Create your own custom map style in the Mapbox Studio style editor following the [Create a custom style](/help/tutorials/create-a-custom-style/) tutorial.
- Work through our [Unity tutorial series](https://www.mapbox.com/unity-sdk/tutorials/) to learn how to create 3D buildings and style those building in a Unity application.
- Try out other [designer styles](https://www.mapbox.com/designer-maps) to find the right one for your project.
