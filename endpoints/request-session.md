# Request an AI Session (POST /api/v1/request-session)

Creates a session for an AI or automation client. The configured access token is required in the `Authorization` header. The session ID is a separate credential and must be kept private.

## Request

```http
POST /api/v1/request-session
Authorization: Bearer <token>
```

No request body is required. The server reads the token only from the Authorization header; values in query parameters or JSON bodies are ignored. Remote requests require HTTPS; localhost requests may use HTTP.

## Successful response

The server returns `201 Created` with a session response. See the [session response fields](/guide/return-objects/session-object.md). The `session` field is used in the JSON body of control, screenshot, and accessibility requests.

## Errors

- `401 Unauthorized`: the Bearer token is absent or invalid.
- `403 Forbidden`: session creation has been disabled by the server operator.
- `429 Too Many Requests`: the server has reached its limit of 500 active sessions.
