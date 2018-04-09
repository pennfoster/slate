---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - http

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction
Penn Foster's integration APIs allow partners and clients to interact with our systems and services through a set of REST endpoints (resources) which provides services like student enrollment, student progression, and account information.

The APIs are hosted on different environments as listed below:

* Test: [https://tst-api-gateway.pennfoster.edu](https://tst-api-gateway.pennfoster.edu)
* Staging: [https://stg-api-gateway.pennfoster.edu](https://stg-api-gateway.pennfoster.edu)
* Production: [https://api-gateway.pennfoster.edu](https://api-gateway.pennfoster.edu)

Each environment also provides a Swagger page by attaching `swagger/ui/index` to the URL.

Email `itdevapp@pennfoster.edu` to request a Developer Key.

## API Endpoints
* All API access is over HTTPS.
* All boolean values should passed as true/false.
* POST and PUT requests, parameters can be sent using standard [HTML form encoding](https://www.w3.org/TR/html4/interact/forms.html#h-17.13.4).
* Optionally, POST and PUT requests may be sent in [JSON format](http://www.json.org/). The content-type of the request must be set to application/json in this case.


# Authentication

> Example OAuth Request:

```javascript
POST https://environment-url/oauth/token

// Request Headers
Authorization: {auth_key}

// Request Body
grant_type=client_credentials&api_key={api_key}
```

>Response (JSON)

```json

{
  "access_token": "<access_token>",
  "token_type": "bearer",
  "expires_in": "<expiration_secs>"
}
```

Penn Foster uses the [OAuth 2.0](https://tools.ietf.org/html/rfc6749) authentication/authorization mechanism. Before making any requests, PF will provide you with the following parameters for each environment: test, staging, and production.

Parameter | Description | Required
--------- | ----------- | --------
grant_type | client_credentials | Yes
client_id | The client_id for your registered application and environment | Yes
client_secret | The client_secret for your registered application and environment | Yes
api_key | The api_key for your registered application and environment | Yes
auth_key | For convenience the auth_key is a base64 encoded client_id:client_secret | No

Penn Foster expects for the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer secretToken`

<aside class="notice">
You must replace <code>secretToken</code> with the token received from the authentication call.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
