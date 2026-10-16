# Guide (GET)

> This is an umbrella endpoint documentation page that covers multiple endpoints. To be specific, it covers all endpoints under `/guide`. It does not refer to `/v1/guide` as it would with other documentation pages for endpoints.

> These endpoints support caching. (see [Guide: Caching](/guide#caching)) 

Requests the server for a documentation page, in Markdown. The main documentation page is at `guide/` (see [Guide](/guide)).

## Body Parameters

No body parameters for this endpoint.

## Example

```http
GET /guide HTTP/1.1
If-None-Match: "17dc0d50ad0fa7bdaebd8f178fe3cc0b5b3a463e3ca5bf21a5e3b90330f2a06e"

HTTP/1.1 304 Not Modified
Date: Sun, 11 Oct 2026 03:47:04 GMT
Cache-Control: no-cache
ETag: "17dc0d50ad0fa7bdaebd8f178fe3cc0b5b3a463e3ca5bf21a5e3b90330f2a06e"
```

## Headers

### Headers inherited from: Caching

`If-None-Match`: **OPTIONAL** The `ETag` of the client's cached file. Compared with the server's current file. If the `ETag` matches, the response will be `304 Not Modified`. Otherwise, it will return `200 OK`. (see [Guide: Endpoint Behavior](/guide#endpoint-behavior))

## Responses

#### 200 OK

##### Returns:

The Markdown page requested by the client, and headers related to caching. (see [Guide: Endpoint Behavior](/guide#endpoint-behavior))

##### Description:

The client did not send `If-None-Match`, or  `If-None-Match` does not match the current file.

### Responses inherited from: Caching

#### 304 Not Modified

##### Returns:

None, and headers related to caching. (see [Guide: Endpoint Behavior](/guide#endpoint-behavior))

##### Description:

`If-None-Match` matched the current resource. (see [Guide: Endpoint Behavior](/guide#endpoint-behavior))