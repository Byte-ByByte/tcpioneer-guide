# Control Endpoint (POST /api/v1/control)

> This endpoint requires an active session. AI sessions also require the Bearer token in the `Authorization` header; local and paired human sessions do not use the API token.

Executes desktop input actions on the host machine. AI token authentication reads only the Authorization header; token values in the URL or JSON body are ignored.

## Request Headers

- `Authorization`: `Bearer <token>` for AI sessions; omit for human sessions.
- `Content-Type`: `application/json`

## Body Parameters

- `session`: `string` (UUID) - Active session ID returned by [`/api/v1/request-session`](/guide/endpoints/request-session.md) or [`/api/v1/human-session`](/guide/endpoints/human-session.md).
- `action`: `object` - The action payload to execute.

### Action Payloads

#### Mouse Move
```json
{
  "session": "<session-key>",
  "action": {
    "action": "mouse.move",
    "x": 500,
    "y": 300
  }
}
```

#### Mouse Click
```json
{
  "session": "<session-key>",
  "action": {
    "action": "mouse.click",
    "button": "left"
  }
}
```

#### Mouse Drag
```json
{
  "session": "<session-key>",
  "action": {
    "action": "mouse.drag",
    "fromX": 100,
    "fromY": 100,
    "toX": 400,
    "toY": 400,
    "button": "left"
  }
}
```

#### Mouse Scroll
```json
{
  "session": "<session-key>",
  "action": {
    "action": "mouse.scroll",
    "amount": -120
  }
}
```

#### Keyboard Press
```json
{
  "session": "<session-key>",
  "action": {
    "action": "keyboard.press",
    "keys": ["CTRL", "C"]
  }
}
```

#### Keyboard Type
```json
{
  "session": "<session-key>",
  "action": {
    "action": "keyboard.type",
    "text": "Hello World!"
  }
}
```

## Responses

### 200 OK
```json
{
  "ok": true,
  "action": {
    "action": "mouse.move",
    "x": 500,
    "y": 300
  }
}
```

### 400 Bad Request
Request body or action parameter is malformed.

### 401 Unauthorized
The session is missing, expired, or not authorized for this request. AI requests also return this status when the Bearer token is absent or invalid.

### 501 Not Implemented
The host platform does not support the requested desktop action.
