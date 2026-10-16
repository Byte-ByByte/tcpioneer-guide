# Request Session (POST)

> This endpoint requires authentication. (see [Guide: Authentication](/guide#authentication))

Requests the server to create a session for the client to use. Returns a [session object](/guide/return-objects/session-object.md), which includes a [session key](/guide#session-key).

## Body Parameters

No body parameters for this endpoint.

## Example
```http
POST /api/v1/request-session
Authorization: Bearer <token>

HTTP/1.1 201 Created
Content-Type: application/json
```

## Headers

### Headers inherited from: Authentication

`Authorization`: `Bearer` token that matches the server's token (see [Guide: Authentication](/guide#authentication)).

## Responses

#### 201 Created

##### Description:

The session body has been created.

##### Returns:

The [session object](/guide/return-objects/session-object). Includes a session key that you may use to operate a session (see [Guide: Session Usage](/guide#session-usage)).

#### 409 Conflict

##### Description:

The server has reached the maximum allowed concurrent sessions in its server policy and the session could not be created.

##### Returns:

None

### Responses inherited from: Authentication

#### 401 Unauthorized

##### Description:

The auth token provided was incorrect or absent.

##### Returns:

None

### Responses inherited from: Server Side Errors

#### 500 Internal Server Error

##### Description:

An issue has happened internally with the TCPIOneer host. Inform an admin if this is a recurring issue.

##### Returns:

None