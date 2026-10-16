# Screenshot Endpoint (POST /api/v1/screenshot)

> This endpoint requires authentication (see [Guide: Authentication](/guide/index.md#authentication)) and an active session key.

Captures a full JPEG screenshot of the host's primary desktop display.

## Request Headers

- `Authorization`: `Bearer <token>`
- `Content-Type`: `application/json`

## Body Parameters

- `session`: `string` (UUID) - Active session key returned by [`/api/v1/request-session`](/guide/endpoints/request-session.md).

```json
{
  "session": "<session-key>"
}
```

## Responses

### 200 OK
- `Content-Type`: `image/jpeg`
- Returns binary JPEG buffer.

### 401 Unauthorized
Invalid token or expired/invalid session key.
