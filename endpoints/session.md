# Session Management (GET & DELETE /api/v1/session)

> These endpoints require authentication (see [Guide: Authentication](/guide#authentication)).

## Inspect Session (GET /api/v1/session)

Inspects information and validity of a given session key.

### Query Parameters

- `session`: `string` (UUID) - Session key to inspect.

Example:
`GET /api/v1/session?session=c8d3ed48-2581-482b-961e-d58a02bced45`

### Response (200 OK)
```json
{
  "ok": true,
  "session": "c8d3ed48-2581-482b-961e-d58a02bced45",
  "createdAt": "2026-10-02T01:09:37.557Z",
  "expiresAt": "2026-10-02T02:09:37.557Z",
  "valid": true
}
```

---

## Delete Session (DELETE /api/v1/session)

Revokes and invalidates a session key immediately.

### Request Body
```json
{
  "session": "c8d3ed48-2581-482b-961e-d58a02bced45"
}
```

### Response (200 OK)
```json
{
  "ok": true,
  "deleted": true
}
```
