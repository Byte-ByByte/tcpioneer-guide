# Control Endpoint (POST /api/v1/control)

> This endpoint requires authentication (see [Guide: Authentication](/guide/index.md#authentication)) and an active session key.

Executes desktop input actions on the host machine.

## Request Headers

- `Authorization`: `Bearer <token>`
- `Content-Type`: `application/json`

## Body Parameters

- `session`: `string` (UUID) - Active session key returned by [`/api/v1/request-session`](/guide/endpoints/request-session.md).
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
Invalid token or expired/invalid session key.
