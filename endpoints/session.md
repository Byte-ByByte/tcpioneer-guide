# Session Management (GET & DELETE /api/v1/session)

AI sessions require the configured Bearer token in the `Authorization` header. The session identifier is a separate value and is not an access token.

## Inspect an AI Session

`GET /api/v1/session?session=<session-id>`

Include `Authorization: Bearer <token>`. The server returns session creation and expiry times. Query strings are omitted from request logs.

## Delete a Session

For an AI session, send its ID in the JSON body and the token in the header:

```http
DELETE /api/v1/session
Authorization: Bearer <token>
Content-Type: application/json

{
  "session": "<session-id>"
}
```

For a human session, omit the Authorization header. The request must still come from that session's permitted local or paired browser connection.

A successful response is:

```json
{
  "ok": true,
  "deleted": true
}
```

Sessions expire after one hour and expired entries are removed automatically. The server permits up to 500 active sessions. Local human sessions need no API token; remote human sessions are created by redeeming a single-use pairing code over HTTPS. The `GET` endpoint inspects AI sessions only.
