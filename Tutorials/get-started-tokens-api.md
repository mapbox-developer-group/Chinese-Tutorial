---
title: Creating access tokens with the Tokens API
description: Walk through creating permanent and temporary access tokens using the Tokens API.
category: Tutorials
level: 2
topics:
- access tokens
language:
- cURL
thumbnail: tokensCurlRequest
prereq: Familiarity with APIs and using the command line.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import UserName from '../../components/username';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

This guide will walk through how to create permanent/public and temporary access tokens with the [Tokens API](https://docs.mapbox.com/api/accounts/#tokens) using cURL. After reading this tutorial, you will be able to create appropriately scoped access tokens with the Tokens API using cURL.

If you're unsure what an access token is or how to use one, read our [access tokens guide](/help/how-mapbox-works/access-tokens/) and [Tokens API documentation](https://docs.mapbox.com/api/accounts/#tokens) for more details.

## Getting started

You will need a couple resources to get started:

- **Mapbox account.** Sign up for free at [mapbox.com/signup](https://www.mapbox.com/signup/).
- **Experience using APIs and the command line with cURL.**

## Decide on your token scopes

Access tokens are keys that allow you to access Mapbox APIs. Every token has one or more token scopes that set the permissions for the token, allowing that access token to do a specific job and interact with specific APIs. For example, if you need to upload data with your new token, you’ll need to select `uploads:write`. Or, if you need your new token to be able to create more access tokens, select `tokens:write`.

If you aren’t sure what scopes you need your new token to have, refer to our [API documentation](https://docs.mapbox.com/api/). Each section lists which scopes are necessary to interact with the specific Mapbox API.

{{
<AppropriateImage imageId="tokenScopes" />
}}

{{
<Note imageComponent={<BookImage />}>
  <p>When you create a new token, some of the scope options are secret scopes. If you add one or more secret scopes to your new token, it will be a secret token. You can only view secret tokens once, at the time when you create them, so it's important to copy the new secret token and save it in a secure place.</p>
</Note>
}}

## Create a token that can create tokens

To create access tokens using the Tokens API, you’ll need to use a token with the `tokens:write` scope. You can create a new token with the `tokens:write` scope on your [access tokens page](https://www.mapbox.com/account/access-tokens).

As an example, a token with the scopes `uploads:read`, `uploads:list`, `uploads:write`, and `tokens:write` would allow you to create tokens that can interact with the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads).

{{
<Note imageComponent={<BookImage />}>
  <p>Every requested scope must be present in the access token used to allow the request. It is not possible to create a token with access to more scopes than the token that created it.</p>
</Note>
}}

Now that you have a token with the `tokens:write` scope, you can use it to create new tokens using the Tokens API.

## Make the token using the command line

### Permanent/public tokens

A permanent or public tokens are access tokens that only have public scopes. In your command line, you can create a permanent/public token by using this command:

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "{token_name}","scopes": ["styles:read", "fonts:read"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

For example, to create a token for interacting with the Uploads API, your command may look like this:

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "Uploads token","scopes": ["styles:tiles", "styles:read", "fonts:read", "datasets:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

Your response will look something like this:

```json
{"client":"api","note":"Uploads token","usage":"sk","id":"cjo6jcmxn0l3x3vqmdr4epqk8","default":false,"scopes":["styles:tiles","styles:read","fonts:read","datasets:read","uploads:read","uploads:write","uploads:list"],"created":"2018-11-07T02:19:53.538Z","modified":"2018-11-07T02:19:53.538Z","token":"{new_access_token}"}
```

Navigate to your [access tokens](https://www.mapbox.com/account/access-tokens) page to see the new token in your account!

### Temporary tokens

Our Tokens API offers the ability to create temporary tokens which expire at a set time. Temporary tokens can be created using public, secret, or even other temporary tokens as long as the authenticating token is scoped correctly. Temporary tokens do not show in your [access tokens page](https://www.mapbox.com/account/access-tokens).

To make temporary tokens, you will need to include `expires` and `scopes` parameters in your API call:

- `expires`: The `expires` parameter should be in [Coordinated Universal Time (UTC)](https://www.timeanddate.com/worldclock/timezone/utc) and specifies when the temporary token will expire. It cannot be a time in the past or more than one hour in the future. If the authorizing token is temporary, the  expires time for the new temporary token cannot be later than that of the authorizing temporary token.
- `scopes`: The `scopes` parameter specifies which scopes that the new temporary token will have. The authorizing token needs to have the same scopes as, or more scopes than, the new temporary token you are creating.

### Creating temporary tokens

In your command line, you can create a temporary token by using this command:


```curl
curl -X POST -d '{"expires": "2018-11-18T06:30:00Z","scopes": ["styles:read", "fonts:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

For example, to create a temporary token for interacting with the Uploads API, your command may look like this:

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "Uploads temp token", "expires": "2018-11-18T06:30:00Z", "scopes": ["styles:tiles", "styles:read", "fonts:read", "datasets:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

Your response should look something like this:

```json
{
  "token": "{new_temporary_token}"

}
```

## Finished product

You have created an access token with the correct scopes using the Tokens API. Go to your [access tokens page](https://www.mapbox.com/account/access-tokens) to find the new token.

## Next steps

Now that you have a token, you can use it according to its scopes.
