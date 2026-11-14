# Delete Session (POST)

> This endpoint requires authentication. (see [Guide: Authentication](/guide#authentication))

> This endpoint requires a Session. (see [Guide: Session Lifecycle](/guide#session-lifecycle))

Deletes a session.

## Body Parameters

`Content-Type: JSON`

* Session 

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

#### 204 No Content

##### Description:

The session has been successfully deleted.

##### Returns:

None

#### 410 Gone

##### Description:

The requested session key has already been deleted.

> **This error is emitted only on the first request that uses a deleted session key. Subsequent requests for the same key return 404 Not Found.** Once you receive this error, you **must** not attempt to use this session key again. (see [Guide: Session Deletion](/guide#session-deletion))

##### Returns:

An [error object](/guide/return-objects/error), which provides more error information.

#### 400 Bad Request

##### Description:

The input is malformed.

##### Returns:

None

#### 404 Not Found

##### Description:

The session key does not exist or is incorrect.

##### Returns:

An [error object](/guide/return-objects/error), which provides more error information.

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