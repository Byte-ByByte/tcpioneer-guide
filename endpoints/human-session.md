# Human Sessions (POST /api/v1/human-session)

Creates a browser session for the human control page at `/pc`. Human sessions do not require the AI API token. The server restricts them to the local browser or a client that redeems a one-use pairing code.

## Connect on the host computer

Open `/pc` on the computer running TCPIOneer and choose **Connect here**. The browser sends:

```http
POST /api/v1/human-session
Content-Type: application/json

{}
```

The request must come from a loopback connection and the same origin as the control page. No `Authorization` header is needed.

## Connect from another computer

Configure the host for HTTPS and open `/pc` locally on the host. Create a pairing code there, then open the host's HTTPS `/pc` URL on the remote computer and redeem the code. The request body is:

```http
POST /api/v1/human-session
Content-Type: application/json

{
  "pairingCode": "A1B2C3D4E5"
}
```

Pairing codes expire after five minutes and can be used once. Redemption requires HTTPS and the same origin as the control page. A paired session is tied to the remote client's IP address; subsequent requests must use HTTPS from that address and origin. See [Pairing codes](/guide/endpoints/pairing.md) for setup and limits.

## Successful response

```json
{
  "ok": true,
  "session": "<session-id>",
  "createdAt": "2026-10-28T12:00:00.000Z",
  "expiresAt": "2026-10-28T13:00:00.000Z",
  "capabilities": ["mouse", "keyboard", "screenshot", "accessibility"]
}
```

Use the returned `session` ID in screenshot, control, accessibility, or session deletion requests. The control page handles this automatically. Human sessions expire after one hour.

## Errors

- `401 Unauthorized`: the supplied pairing code is invalid, expired, already used, or the request is not over HTTPS.
- `403 Forbidden`: a remote client did not supply a pairing code, or the request origin is not permitted.
- `429 Too Many Requests`: the active-session limit has been reached.
