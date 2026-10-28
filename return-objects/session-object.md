# Session Responses

Session IDs are opaque values used to authorize requests. They are separate from the API access token. AI sessions require the Bearer token in the `Authorization` header when used; local and paired human sessions are authorized by the browser connection and do not use the API token.

## Create an AI session

`POST /api/v1/request-session` returns `201 Created`:

```json
{
  "ok": true,
  "session": "c8d3ed48-2581-482b-961e-d58a02bced45",
  "session-key": "c8d3ed48-2581-482b-961e-d58a02bced45",
  "createdAt": "2026-10-28T12:00:00.000Z",
  "created": "2026-10-28T12:00:00.000Z",
  "expiresAt": "2026-10-28T13:00:00.000Z",
  "expiry": "2026-10-28T13:00:00.000Z",
  "capabilities": ["mouse", "keyboard", "screenshot", "accessibility"],
  "usable": true
}
```

Use `session` in the JSON body of control, screenshot, and accessibility requests. `session-key`, `created`, and `expiry` are compatibility aliases. AI sessions expire one hour after creation.

## Create a human session

`POST /api/v1/human-session` returns `201 Created` with `ok`, `session`, `createdAt`, `expiresAt`, and `capabilities`. It does not return the AI-only `session-key` and compatibility aliases. See [Human Sessions](/guide/endpoints/human-session.md).

## Inspect an AI session

`GET /api/v1/session?session=<session-id>` returns:

```json
{
  "ok": true,
  "session": "c8d3ed48-2581-482b-961e-d58a02bced45",
  "createdAt": "2026-10-28T12:00:00.000Z",
  "expiresAt": "2026-10-28T13:00:00.000Z",
  "valid": true
}
```

This endpoint requires the Bearer token and only inspects AI sessions. See [Session Management](/guide/endpoints/session.md).
