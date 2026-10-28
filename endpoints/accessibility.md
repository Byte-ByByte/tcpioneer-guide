# Accessibility Endpoint (POST /api/v1/accessibility)

Returns a bounded tree of visible Windows UI Automation elements for an AI or human session. AI sessions require the Bearer token in the `Authorization` header. Human sessions use the local or paired browser session and do not need an API token.

## Request

```http
POST /api/v1/accessibility
Authorization: Bearer <token>
Content-Type: application/json

{
  "session": "<session-id>",
  "maxNodes": 250,
  "maxDepth": 5
}
```

For a human session, omit the `Authorization` header and use its session ID. The server checks that the request matches the local or paired session's origin and connection.

- `session`: required session ID.
- `maxNodes`: optional integer from 1 to 500; defaults to 250.
- `maxDepth`: optional integer from 1 to 8; defaults to 5.

## Response

```json
{
  "ok": true,
  "tree": {
    "name": "Desktop",
    "role": "ControlType.Pane",
    "automationId": "",
    "enabled": true,
    "bounds": {
      "x": 0,
      "y": 0,
      "width": 1920,
      "height": 1080
    },
    "children": []
  }
}
```

Each node contains `name`, `role`, `automationId`, `enabled`, `bounds` (`x`, `y`, `width`, `height`), and `children`. Offscreen elements are skipped. Names are limited to 160 characters and automation IDs to 128 characters. Password controls are labeled `[password]`; field values are not included.

## Errors

- `400 Bad Request`: `maxNodes` or `maxDepth` is outside its allowed range, or the request body is invalid.
- `401 Unauthorized`: the session is missing, expired, or not authorized for this request.
- `501 Not Implemented`: Windows UI Automation is unavailable on this host.
