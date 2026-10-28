# Pairing Codes (POST /api/v1/pairing)

Creates a one-use code so a person on another computer can open a tokenless human-control session. Pairing is initiated from the host computer's local `/pc` page and redeemed from the remote computer over HTTPS.

## Create a code

On the host, open `/pc` and select **Create pairing code**. The page sends:

```http
POST /api/v1/pairing
Content-Type: application/json

{}
```

The request must come from a loopback connection and the same origin as the host control page. No API token is required.

## Response

```json
{
  "ok": true,
  "pairingCode": "A1B2C3D4E5",
  "expiresAt": "2026-10-28T12:05:00.000Z"
}
```

The code is ten hexadecimal characters, expires after five minutes, and is consumed by the first successful redemption. Give it only to the person you intend to connect. The server allows up to 20 active codes and limits redemption attempts to eight per client IP address per minute.

Redeem the code on the remote computer through the host's HTTPS `/pc` page. The remote client must use a trusted TLS certificate and the same origin as that page. See [Human sessions](/guide/endpoints/human-session.md).

## Errors

- `403 Forbidden`: the request did not come from the local host control page.
- `429 Too Many Requests`: the server already has 20 active pairing codes.
