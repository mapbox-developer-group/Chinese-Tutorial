---
title: Upload to Mapbox using cURL
description: Learn how to use the Mapbox Uploads API.
thumbnail: uploadCurl
level: 3
topics:
- uploads
language:
- cURL
prereq: Familiarity with cURL.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
contentType: tutorial
---

{{<Note title='Beta feature: Upload vector tilesets with the Tilesets API' imageComponent={<BookImage />}>}}

The [Mapbox Tilesets API](https://docs.mapbox.com/api/maps/#tilesets) has several beta endpoints that allow you to create custom vector tilesets. As an alternative to the Uploads API process outlined in this tutorial, you can use these endpoints for tiling vector data using custom configuration rules. While these endpoints are in beta, they are subject to potential changes.

{{</Note>}}

This guide illustrates how you can use the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) via the command line with cURL. If you would like to upload your data through a point-and-click interface, you can do so with [Mapbox Studio](https://www.mapbox.com/studio-manual/overview/geospatial-data/).

## Getting started

There are a few resources you'll need before getting started:

- **Mapbox account**. Sign up for free at [mapbox.com/sign-up](https://www.mapbox.com/studio).
- [**A secret access token**](https://www.mapbox.com/account/access-tokens) with `uploads:write` scope enabled.
- The [**AWS CLI**](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) (requires Python and pip).
- [**cURL**](http://curl.haxx.se/download.html).
- Data to upload &mdash; see our [accepted file types here](/help/troubleshooting/uploads/#accepted-file-types-and-transfer-limits).

## Stage your file on Amazon S3

Mapbox provides an Amazon S3 bucket to stage your file while your upload is processed. All uploads must be staged in this bucket before being uploaded to your Mapbox account. To stage a file on S3, you'll need to retrieve temporary credentials from the Uploads API's `credentials` endpoint:


```
curl -X POST https://api.mapbox.com/uploads/v1/username/credentials?access_token=<secret access token>
```

In the above command, `secret_access_token` is your secret [access token](/help/glossary/access-token/) and `username` is your Mapbox account username.

If your request URL is valid, you should receive a response that looks something like this:

```
{
  "accessKeyId": "{accessKeyId}",
  "bucket": "{bucket}",
  "key": "{key}",
  "secretAccessKey": "{secretAccessKey}",
  "sessionToken": "{sessionToken}",
  "url": "{url}"
}
```

These credentials give you permission to stage your data on Amazon's servers and are crucial to the next step. Enter the following into your terminal to set the correct environment variables that allow you to upload your data to S3:

```
$ export AWS_ACCESS_KEY_ID={accessKeyId}
$ export AWS_SECRET_ACCESS_KEY={secretAccessKey}
$ export AWS_SESSION_TOKEN={sessionToken}
```

To stage your data on S3, run the following in your terminal:

```
$ aws s3 cp /path/to/file s3://{bucket}/{key} --region us-east-1
```

You should see a response that looks like:

```
upload: ./{file name} to s3://{bucket}/{key}
```

## Begin the upload process

Once your file is staged on Amazon S3, you need to *create an upload* that defines where the Mapbox Uploads API should look for your staged data. The *upload* is not the file itself, but an object that tells Mapbox's servers how to find your staged file and where to put it. You give Mapbox instructions by sending a `POST` request with this information. Using cURL, your request will look like:

```
curl -X POST -H "Content-Type: application/json" -H "Cache-Control: no-cache" -d '{
  "url": "http://{bucket}.s3.amazonaws.com/{key}",
  "tileset": "{username}.{tileset-name}"
}' 'https://api.mapbox.com/uploads/v1/{username}?access_token=secret_access_token'
```

**Note:** The `{username}` is always your Mapbox username. The `{tileset-name}` parameter is what you would like to call your data when it gets to Mapbox, such as `bike-trails` or `airports`. If you use the name of an existing tileset, it will be overwritten.

Once a successful `POST` request has completed, you will receive an [`HTTP 201`](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#2xx_Success) response and a confirmation that your upload has started, which will look like this:

```
{
  "complete": false,
  "tileset": "{username}.{tileset-name}",
  "error": null,
  "id": "{upload-id}",
  "name": "{username}-{tileset-name}",
  "modified": "{timestamp}",
  "created": "{timestamp}",
  "owner": "{username}",
  "progress": 0
}
```

**Note:** The `{upload-id}` refers to the upload's unique identifier. This can be used to [retrieve the upload status](https://docs.mapbox.com/api/maps/#retrieve-upload-status) later.

## Finished product

Once you have started the upload process, it may be a few minutes before your upload has finished processing and is complete. This is dependent on the size and complexity of your data. If your upload fails, see our [uploads troubleshooting guide](/help/troubleshooting/uploads/#errors) for more information.

If the upload is successful, your new tileset will be listed on your [tilesets page](https://www.mapbox.com/studio/tilesets). At this point, your tileset is now available to use in custom map styles!
