# TCPIOneer Guide

## Introduction
Welcome to **TCPIOneer**, an API that serves as a **remote-desktop host** controlled via **HTTP endpoints**.

This guide covers:
* Authentication
* Session lifecycle
* Capabilities
* Endpoints

TCPIOneer allows clients (automation scripts, HTTP callers, or AI agents) to control desktop input and take screenshots.

## Guide Directory

All documentation paths under `/guide` are accessible without authentication.

* [Guide Index](/guide/index.md)
* Endpoints
  * [Request Session (/api/v1/request-session)](/guide/endpoints/request-session.md)
  * [Control Desktop (/api/v1/control)](/guide/endpoints/control.md)
  * [Capture Screenshot (/api/v1/screenshot)](/guide/endpoints/screenshot.md)
  * [Session Info & Deletion (/api/v1/session)](/guide/endpoints/session.md)
* Capabilities
  * [Host Capabilities](/guide/capabilities.md)
* Return Objects
  * [Session Object](/guide/return-objects/session-object.md)

## Authentication
To access remote desktop endpoints, pass the server token in the `Authorization` header as a `Bearer` token.

Example:
```http
POST /api/v1/request-session HTTP/1.1
Authorization: Bearer abcd1234
```

> **Note:** Configure or rotate the token in `config.json`.

## Session Lifecycle
Sessions provide the authorization context to control the desktop.

1. **Request Session:** Call `POST /api/v1/request-session` with your Bearer token.
2. **Use Session:** Pass the returned `session` key in POST bodies for `/api/v1/control` and `/api/v1/screenshot`.
3. **Delete Session:** Call `DELETE /api/v1/session` when finished to free server resources.

## Capabilities
TCPIOneer supports:
* **Mouse control:** Move, click, drag, scroll.
* **Keyboard control:** Key combinations and unicode text typing.
* **On-demand screenshots:** Full display JPEG screenshot capture.

For details, see [Host Capabilities](/guide/capabilities.md).
