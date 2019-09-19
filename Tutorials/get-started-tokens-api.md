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

本指南将演示如何使用 cURL 通过 [Tokens API](https://docs.mapbox.com/api/accounts/#tokens) 创建永久的、公共的和临时的 access token。阅读本教程后，你将能够使用 cURL 通过 Tokens API 创建作用域范围恰当的 access token。

如果你不确定 access token 是什么，或者如何使用它，请阅读 [access tokens guide](/help/how-mapbox-works/access-tokens/) 和 [Tokens API documentation](https://docs.mapbox.com/api/accounts/#tokens) 获取更多信息。

## 入门

以下是入门前需要的一些资源：

- **Mapbox 账号。** 在 [mapbox.com/signup](https://www.mapbox.com/signup/) 注册一个免费账号。
- **拥有通过 cURL 使用 API 和命令行的经验。**

## 决定 token 作用域

Access token 是允许你访问 Mapbox API 的密钥。每个 token 有一个或多个 token 作用域，用于设置它的权限，允许它执行特定作业并与特定 API 进行交互。例如，如果你需要使用新 token 上传数据，则需要选择 `uploads:write`。或者，如果你需要新 token 能创建更多 access token，请选择 `tokens:write`。

如果你不确定新的 token 需要什么作用域，请查阅 [API documentation](https://docs.mapbox.com/api/)。 每个部分列出了与特定 Mapbox API 交互所需的作用域。

{{
<AppropriateImage imageId="tokenScopes" />
}}

{{
<Note imageComponent={<BookImage />}>
  <p>当你创建新 token 时，某些作用域选项是机密作用域。如果你给新的 token 增加一个或多个机密作用域，它就会是一个机密 token。只有在创建它们的时候，你才能查看一次机密 token。因此，复制新的机密 token 并将其保存在一个安全的地方很重要。</p>
</Note>
}}

## 创建一个 token，它能新建其他 token

使用 Tokens API 创建 access token，你需要用的 token 需具备 `tokens:write` 作用域。在 [access tokens page](https://www.mapbox.com/account/access-tokens) 上，你可以创建一个具有 `tokens:write` 作用域的新 token。

例如, 一个具有 `uploads:read`、 `uploads:list` 、 `uploads:write` 和 `tokens:write` 这些作用域的 token，使你创建能与 [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) 交互的 token。

{{
<Note imageComponent={<BookImage />}>
  <p>每个必要的作用域都必需存在于 access token，用它来通过请求。用一个 token 创建另一个更多作用域的 token，这是不可能的。</p>
</Note>
}}

现在，你有一个具有 `tokens:write` 作用域的 token，你可以使用它通过 Tokens API 创建新的 token。

## 使用命令行创建 token

### 永久 token、公共 token

永久 token 或公共 token 是仅具有公共作用域的 access token。在命令行中，你可以通过如下命令创建永久、公共 token：

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "{token_name}","scopes": ["styles:read", "fonts:read"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

例如，创建一个能与 Uploads API 交互的 token，命令会是这样：

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "Uploads token","scopes": ["styles:tiles", "styles:read", "fonts:read", "datasets:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

得到的回复大概会是这样：

```json
{"client":"api","note":"Uploads token","usage":"sk","id":"cjo6jcmxn0l3x3vqmdr4epqk8","default":false,"scopes":["styles:tiles","styles:read","fonts:read","datasets:read","uploads:read","uploads:write","uploads:list"],"created":"2018-11-07T02:19:53.538Z","modified":"2018-11-07T02:19:53.538Z","token":"{new_access_token}"}
```

打开 [access tokens](https://www.mapbox.com/account/access-tokens) 页面，查看你账号中的新 token。

### 临时 token

Tokens API 提供了创建临时 tokens 的能力，使其在设定的时间失效。只要正确限定身份验证 token 的作用域，临时 token 可以用公共 token、机密 token 甚至其他临时 token 创建。临时 token 不会在 [access tokens page](https://www.mapbox.com/account/access-tokens) 显示。

要创建临时 token，你需要在 API 调用中包含 `expires` 和 `scopes` 这两个参数:

- `expires`: `expires` 参数需要是 [Coordinated Universal Time (UTC)](https://www.timeanddate.com/worldclock/timezone/utc) ，并指定临时 token 何时过期。它不能是过去的时间，也不能是未来一小时以外的时间。如果授权 token 是临时的，新临时 token 的过期时间不能晚于授权 token 的过期时间。
- `scopes`: `scopes` 参数指定新临时 token 将具有何种作用域。授权 token 的作用域要与新创建的临时 token 的作用域一致或比其更多。

### 创建临时 token

在命令行中，可以使用此命令创建临时 token：


```curl
curl -X POST -d '{"expires": "2018-11-18T06:30:00Z","scopes": ["styles:read", "fonts:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

例如，创建一个能与 Uploads API 交互的临时 token，命令会是这样：

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "Uploads temp token", "expires": "2018-11-18T06:30:00Z", "scopes": ["styles:tiles", "styles:read", "fonts:read", "datasets:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

得到的回复大概会是这样：

```json
{
  "token": "{new_temporary_token}"

}
```

## 成品

你已经使用 Tokens API 创建了具有正确作用域的 access token。打开 [access tokens page](https://www.mapbox.com/account/access-tokens) 页面查看新的 token。

## 下一步

现在，你有了一个 token，你可以根据它的作用域使用它。
