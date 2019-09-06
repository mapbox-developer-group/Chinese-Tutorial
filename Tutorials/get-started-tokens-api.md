---
title: 使用 Tokens API 创建访问令牌
description: 使用 Tokens API 演示创建永久和临时访问令牌
category: Tutorials
level: 2
topics:
- access tokens
language:
- cURL
thumbnail: tokensCurlRequest
prereq: 熟悉 API 并使用命令行
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import UserName from '../../components/username';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

本指南将演示如何通过 cURL 使用 [Tokens API](https://docs.mapbox.com/api/accounts/#tokens) 创建永久/公共和临时访问令牌。阅读本教程后，你将能够通过 cURL 使用 Tokens API 创建适当作用域的访问令牌。

如果你不确定访问令牌是什么，或者如何使用它，请阅读 [access tokens guide](/help/how-mapbox-works/access-tokens/) 和 [Tokens API documentation](https://docs.mapbox.com/api/accounts/#tokens) 获取更多信息。

## 入门

以下是入门前需要的一些资源：

- **Mapbox 账号。** 在 [mapbox.com/signup](https://www.mapbox.com/signup/) 注册一个免费账号。
- **拥有通过 cURL 使用 API 和命令行的经验。**

## 决定你的令牌作用域

访问令牌是允许你访问 Mapbox API 的密钥。每个令牌都有一个或多个令牌作用域，用于设置令牌的权限，允许该访问令牌执行特定作业并与特定 API 进行交互。例如，如果你需要使用新令牌上传数据，则需要选择 `uploads:write`。或者，如果你需要新令牌创建更多可访问令牌，请选择 `tokens:write`。

如果你不确定新的令牌需要什么作用域，请查阅 [API documentation](https://docs.mapbox.com/api/)。 每个部分列出了与特定 Mapbox API 交互所需的作用域。

{{
<AppropriateImage imageId="tokenScopes" />
}}

{{
<Note imageComponent={<BookImage />}>
  <p>当你创建新令牌时，某些作用域选项是机密作用域。如果你给新的令牌增加一个或多个机密作用域，它就会是一个机密令牌。只有在创建它们的时候，你才能查看一次机密令牌。因此，复制新的机密令牌并将其保存在一个安全的地方很重要。</p>
</Note>
}}

## 创建一个能创建其他令牌的令牌

使用 Tokens API 创建访问令牌，你需要用 `tokens:write` 作用域的令牌。在 [access tokens page](https://www.mapbox.com/account/access-tokens) 上，你可以创建一个具有 `tokens:write` 作用域的新令牌。

例如, 一个具有 `uploads:read`、 `uploads:list` 、 `uploads:write` 和 `tokens:write` 的令牌，会允许你创建能与 [Mapbox Uploads API](https://docs.mapbox.com/api/maps/#uploads) 交互的令牌。

{{
<Note imageComponent={<BookImage />}>
  <p>每个请求的作用域都必须存在于用于允许请求的访问令牌中。用一个令牌创建另一个更多作用域的令牌，这是不可能的 。</p>
</Note>
}}

现在，你有一个具有 `tokens:write` 作用域的令牌，你可以使用它通过 Tokens API 创建新的令牌。

## 使用命令行创建令牌

### 永久/公共令牌

永久令牌或公共令牌是仅具有公共作用域的访问令牌。在命令行中，你可以通过如下命令创建永久/公共令牌：

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "{token_name}","scopes": ["styles:read", "fonts:read"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

例如，创建一个能与 Uploads API 交互的令牌，命令会是这样：

```curl
curl -H "Content-Type: application/json" -X POST -d '{"note": "Uploads token","scopes": ["styles:tiles", "styles:read", "fonts:read", "datasets:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

得到的回复大概会是这样：

```json
{"client":"api","note":"Uploads token","usage":"sk","id":"cjo6jcmxn0l3x3vqmdr4epqk8","default":false,"scopes":["styles:tiles","styles:read","fonts:read","datasets:read","uploads:read","uploads:write","uploads:list"],"created":"2018-11-07T02:19:53.538Z","modified":"2018-11-07T02:19:53.538Z","token":"{new_access_token}"}
```

导航到 [access tokens](https://www.mapbox.com/account/access-tokens) 页面，查看你账号中的新令牌。

### 临时令牌

Tokens API 提供了创建临时令牌的能力，使其在设定的时间失效。只要正确限定身份验证令牌的作用域，临时令牌可以用公共令牌、机密令牌甚至其他临时令牌创建。临时令牌不会在 [access tokens page](https://www.mapbox.com/account/access-tokens) 显示。

要创建临时令牌，你需要在 API 调用中包含 `expires` 和 `scopes` 这两个参数:

- `expires`: `expires` 参数需位于 [Coordinated Universal Time (UTC)](https://www.timeanddate.com/worldclock/timezone/utc) 中，并指定临时令牌何时过期。它不能是过去的时间，也不能是未来一小时以外的时间。如果授权令牌是临时的，新临时令牌的过期时间不能晚于该令牌的过期时间。
- `scopes`: `scopes` 参数指定新临时令牌将具有何种作用域。授权令牌要具有与新创建的临时令牌同样多的作用域，或要比其更多。

### 创建临时令牌

在命令行中，可以使用此命令创建临时令牌：


```curl
curl -X POST -d '{"expires": "2018-11-18T06:30:00Z","scopes": ["styles:read", "fonts:read", "uploads:read", "uploads:write", "uploads:list"]}' 'https://api.mapbox.com/tokens/v2/{{<UserName />}}?access_token={{<UserAccessToken/>}}'
```

例如，创建一个能与 Uploads API 交互的临时令牌，命令会是这样：

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

你已经使用 Tokens API 创建了具有正确作用域的访问令牌。转到 [access tokens page](https://www.mapbox.com/account/access-tokens) 页面查找令牌。

## 下一步

现在，你有了一个令牌，你可以根据它的作用域使用它。
