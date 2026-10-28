# TCPIOneer AI API

TCPIOneer exposes versioned HTTP endpoints under `/api/v1`. There is no `/ai` URL prefix. The API can capture screenshots, return a bounded Windows accessibility tree, and perform mouse and keyboard actions.

## Authentication

AI API calls that create or use an AI session require the configured token in the `Authorization` header:

```http
Authorization: Bearer <token>
```

Authentication reads the token only from the Authorization header; token values in URLs or JSON bodies are ignored. Request logs contain route paths only and redact the configured token from errors. Localhost AI requests may use HTTP; remote AI requests require HTTPS.

The Electron app generates a random token and stores it in its per-user `config.json`. If a CLI config file has a missing or shorter-than-32-character `security.token`, startup generates a random token and saves it there. Keep that config private.

## Endpoints

- `GET /api/v1/health` — unauthenticated liveness check.
- `GET /api/v1/capabilities` — unauthenticated capability and endpoint list.
- `POST /api/v1/request-session` — create an AI session; requires the Bearer header.
- `POST /api/v1/control` — perform a mouse or keyboard action; requires the Bearer header and session.
- `POST /api/v1/screenshot` — capture a JPEG; requires the Bearer header and session.
- [`POST /api/v1/accessibility`](/guide/endpoints/accessibility.md) — return a bounded UI Automation tree.
- [`GET /api/v1/session?session=<session-id>` and `DELETE /api/v1/session`](/guide/endpoints/session.md) — inspect or delete a session.
- [`POST /api/v1/human-session`](/guide/endpoints/human-session.md) — create a tokenless local human session or redeem a remote pairing code.
- [`POST /api/v1/pairing`](/guide/endpoints/pairing.md) — create a short-lived code from the host computer's local control page.
- `POST /api/v1/execute` — returns `410 Gone`; arbitrary shell command execution is disabled.

Sessions expire after one hour. The server removes expired sessions automatically and limits the active-session count.

## Create an AI session

```http
POST /api/v1/request-session
Authorization: Bearer <token>
```

The response contains a session ID. Send it in the `session` JSON property on control, screenshot, and accessibility requests.

## Control the desktop

```http
POST /api/v1/control
Authorization: Bearer <token>
Content-Type: application/json

{
  "session": "<session-id>",
  "action": {
    "action": "mouse.click",
    "button": "left"
  }
}
```

Supported actions are `mouse.move`, `mouse.click`, `mouse.drag`, `mouse.scroll`, `keyboard.press`, and `keyboard.type`.

## Capture a screenshot

```http
POST /api/v1/screenshot
Authorization: Bearer <token>
Content-Type: application/json

{
  "session": "<session-id>",
  "maxWidth": 1920,
  "quality": 65
}
```

The response body is a JPEG image. `maxWidth` can be 320–3840 and `quality` can be 30–90. The response also includes `X-Desktop-Width`, `X-Desktop-Height`, `X-Desktop-Left`, and `X-Desktop-Top` headers so clients can map a resized screenshot back to the Windows virtual desktop, including multi-monitor offsets.

## Read the accessibility tree

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

The response contains visible Windows UI Automation nodes with role, name, automation ID, enabled state, bounds, and children. Password fields are labeled `[password]`; field values are not returned. The response is limited to 500 nodes and depth 8.

## Human control without an API token

On the host computer, open `/pc` and choose **Connect here**. The page creates a tokenless session restricted to the local computer and the same origin.

For another computer, configure HTTPS first and bind the server to the network. Use a TLS certificate trusted by the remote device and valid for the remote hostname and `localhost` (used by the desktop app). The host operator opens `/pc` locally and chooses **Create pairing code**. Redeem that one-use code on the remote computer's HTTPS `/pc` page. Codes expire after five minutes; the server allows 20 active codes and limits redemption to eight attempts per client IP address per minute. The paired session is tied to the remote client's IP address and same origin. See the [human-session endpoint details](/guide/endpoints/human-session.md).

Example server configuration:

```json
{
  "server": {
    "host": "0.0.0.0",
    "port": 3420,
    "tls": {
      "cert": "C:/certs/tcpioneer-fullchain.pem",
      "key": "C:/certs/tcpioneer-key.pem"
    },
    "publicUrl": "https://desktop.example.com:3420"
  }
}
```

For the Electron installer, edit `%APPDATA%\tcpioneer\config.json` while TCPIOneer is closed. For the CLI, put the settings in its `config.json`. Preserve the generated `security.token`. Use a certificate trusted by the remote devices; do not expose the service over plain HTTP.
