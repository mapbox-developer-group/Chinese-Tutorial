---
title: Customize label text for a single label
description: Use expressions in Mapbox Studio to alter a single label.
thumbnail: customizeLabelText
level: 1
topics:
- data
- map design
language:
- No code
contentType: tutorial
prependJs:
  - "import AppropriateImage from '../../components/appropriate-image';"
---

This tutorial will walk you through how to use expressions in the **Mapbox Studio style editor** to customize the label text for a single label.

## Getting started

Before getting started, you will need to create a **Mapbox account** to use the Mapbox Studio style editor. You can create an account at [mapbox.com/account](https://account.mapbox.com).

## Create a new style

Log into your Mapbox account and navigate to your [Styles page](https://studio.mapbox.com/styles). This is where all your styles are listed. A [style](/help/glossary/style/) is a set of rules for how Mapbox will draw your map on the page. It defines how all your data should be styled and includes references to your data and map images (icons, markers, patterns), fonts. For more about styles, see the [Styles](https://docs.mapbox.com/studio-manual/reference/styles/) section of the Mapbox Studio Manual.

Go to your [Styles page](https://studio.mapbox.com). Click the **New style** button. Find the _Basic Template_ style and click **Customize Basic Template**. The style editor will automatically open with the Basic template style ready for editing.

## Use the style editor

The **Mapbox Studio style editor** is a visual tool for creating custom map styles to your exact specifications. Take a look at the layers on the left side of the style editor screen. Each layer can be customized in a variety of ways including (but not limited to) changing labels.

## Use expressions to edit specific labels within a layer

Click on the **country-label** layer to see all the options available to style this layer. To customize the country labels based on conditions and properties within the data, select **Style with data conditions** and choose `name_en` to style the label based on the English name for the country.

{{
  <AppropriateImage
    imageId="customizeLabelText1"
    alt="Mapbox Studio screenshot of 'Style with data conditions'"
  />
}}

In the new panel, you are prompted to fill in the details of your data condition. In the first text field, enter `France` since this is the label you will be customizing. In the `Text field`, add `"Land in: "` and click on **&** to combine your two strings. As you do this, you will see the `France` label change to `Land in: France` on your map.

{{
  <AppropriateImage
    imageId="customizeLabelText2"
    alt="Mapbox Studio screenshot of data conditions panel"
  />
}}

To edit another data condition, click **Done** in the bottom right hand corner and then **Add another condition**. This time, continue the travel journey by choosing the first stop on the trip. In the first text field, enter `Spain` and then `"First stop: "` in the `Text field` box.

{{
  <AppropriateImage
    imageId="customizeLabelText3"
    alt="Mapbox Studio screenshot of data conditions panel"
  />
}}

Repeat the previous step to continue to add more data conditions and stops on the trip. Once you are finished your map will look something like the one below.

{{
  <AppropriateImage
    imageId="customizeLabelText4"
    alt="Mapbox Studio screenshot of completed data conditions"
  />
}}

## Final product

You've updated your map using expressions to display custom labels for specific labels. To learn more about using the Mapbox Studio style editor, read the [Mapbox Studio Manual](https://docs.mapbox.com/studio-manual/).

{{
  <AppropriateImage
    imageId="customizeLabelTextFinal"
    alt="final product with customized labels"
  />
}}
