---
title: Access tokens
description: Learn how access tokens work and how to create and manage your access tokens.
image: /img/narrative/access-token.svg
topics:
  - access tokens
prependJs:
  - "import ChevronousText from '@mapbox/mr-ui/chevronous-text';"
contentType: guide
---

To use any of Mapbox's tools, APIs, or SDKs, you'll need a Mapbox [access token](/help/glossary/access-token). Mapbox uses access tokens to associate API requests with your account. You can find your access tokens, create new ones, or delete existing ones on your [Access Tokens page](https://account.mapbox.com/access-tokens)  or programmatically using the [Mapbox Tokens API](https://docs.mapbox.com/api/accounts/#tokens).

## How access tokens work

### Scopes

Each access token you create will have a set of permissions that allow you to make certain types of requests to Mapbox APIs -- these are called **scopes**. Some Mapbox APIs only accept requests that include tokens with a particular scope. When creating an access token, you will have the option to add additional [public or private scopes](/help/glossary/access-token) to your token. If you choose to add any secret scopes to your token, you will have only one chance to view the token.

When choosing scopes, consider what you plan to do with the token. **To protect your account and your data, do not grant more scopes than necessary to each token**. For example, if you are creating a token to upload data to Mapbox with the [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads), you will want to make sure you select the `uploads:write` and `uploads:read` scopes. To display a map in a web or mobile application, you should create a _separate_ access token that does not include the private uploads-related scopes, but does include the public `styles:read` and `fonts:read` scopes.

Our [API documentation](https://docs.mapbox.com/api/) lists the scopes required for each Mapbox API. **For a complete list of available scopes see the [Account documentation](/help/account/tokens/).**

### URL restrictions

You can make your access tokens more secure by adding URL restrictions. When you add a URL restriction to a token, that token will only work for requests that originate from the URLs you specify. Tokens without restrictions will work for requests originating from any URL. 

**For more information on requirements and details for implementing URL restrictions, see the [Account documentation](/help/account/tokens/).**

### Token rotation

Any public [access tokens](/help/glossary/access-token) you include in webpage will be visible to anyone who makes an effort to look for it. Access tokens can be deleted and rotated at any time if you suspect misuse. Secret tokens should only be used in places where they will not be visible to your users.

You can create as many access tokens as you want. To rotate, [create a new access token](#creating-and-managing-access-tokens), replace it in a project, and then remove the old token. Invalidation for uncached requests will happen immediately. Cached requests can take up to an hour.


## Creating and managing access tokens

There are two options for creating and managing Mapbox access tokens: use the Tokens page in your Mapbox Account to manage tokens using a UI or use the Tokens API to create, read, and update tokens programmatically.  

### Mapbox Account Dashboard

Access tokens can be created, deleted, and managed on your [Access Tokens page](https://account.mapbox.com/access-tokens):

1. Click **Create a token** and give your new token a name to help you remember its purpose.
2. Specify scopes.

![Example secret access token](/help/img/account/access-token-scopes.png)

3. Click **Create token** to create the token. You may be prompted to re-enter your password.
4. Success! Your new token will appear at the top of your list of tokens.

You can click on the name of any token to see the scopes it covers and, if the token is public, you can see the token itself.

If you created a secret access token, you will only be able to see the token in your account dashboard once - be sure to store it somewhere safe (like a password manager) if you need to access it later.

![Example secret access token](/help/img/account/example-access-token.png)

### Mapbox Tokens API

With the [Mapbox Tokens API](https://docs.mapbox.com/api/accounts/#tokens) you can create, read, and update your access tokens. To create additional tokens using this API you will first need to create an initial token with the `tokens:write` scope and any scopes you want to add to the created token. To create this initial token visit your [Access Tokens page](https://account.mapbox.com/access-tokens), and click **Create a token**. Read more about the Tokens API on our [API documentation page](https://docs.mapbox.com/api/).
