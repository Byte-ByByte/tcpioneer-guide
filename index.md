# TCPIOneer Guide

## Introduction

TCPIOneer is a Windows remote-desktop host with an HTTP API for desktop control, screenshots, and accessibility information. AI and automation clients use the versioned API under `/api/v1`; the human control page is at `/pc`. There is no `/ai` API prefix.

## Guide Directory

All documentation paths under `/guide` are available without authentication.

- [Guide Index](/guide/index.md)
- [AI API Reference](/guide/ai-api.md)
- [Windows installation and configuration](/guide/installing.md)
- [Capabilities](/guide/capabilities.md)
- Endpoints
  - [Request an AI session](/guide/endpoints/request-session.md)
  - [Control the desktop](/guide/endpoints/control.md)
  - [Capture a screenshot](/guide/endpoints/screenshot.md)
  - [Read accessibility information](/guide/endpoints/accessibility.md)
  - [Create a human session](/guide/endpoints/human-session.md)
  - [Create a pairing code](/guide/endpoints/pairing.md)
  - [Inspect or delete a session](/guide/endpoints/session.md)
- [Session response fields](/guide/return-objects/session-object.md)

## Authentication

AI and automation clients send the configured token only in the `Authorization` header:

```http
POST /api/v1/request-session HTTP/1.1
Authorization: Bearer <token>
```

Authentication reads the token only from the Authorization header; token values in URLs and JSON request bodies are ignored. The token is stored as `security.token` in `config.json`; request logs omit query strings and credentials. Localhost AI requests may use HTTP. Remote AI requests require HTTPS.

The human control page at `/pc` does not ask for the API token. A same-origin browser on the host computer can connect locally. Connecting from another computer uses a one-use pairing code over HTTPS. See [Human sessions](/guide/endpoints/human-session.md) and [Pairing codes](/guide/endpoints/pairing.md).

## AI Session Lifecycle

1. **Create:** Call `POST /api/v1/request-session` with the Bearer header.
2. **Use:** Send the returned `session` ID in the JSON body to `/api/v1/control`, `/api/v1/screenshot`, and `/api/v1/accessibility`.
3. **Delete:** Call `DELETE /api/v1/session` with the session ID in the JSON body and the Bearer header.

AI sessions expire after one hour. The server periodically removes expired sessions and allows up to 500 active sessions.

## Capabilities

TCPIOneer supports:

- **Mouse:** Move, click, drag, and scroll.
- **Keyboard:** Press key combinations and type Unicode text.
- **Screenshots:** Capture a resizable JPEG of the Windows virtual desktop with coordinate metadata.
- **Accessibility:** Read a bounded Windows UI Automation tree. Password fields are marked and their values are not returned.

For request formats and limits, see the [AI API Reference](/guide/ai-api.md).
