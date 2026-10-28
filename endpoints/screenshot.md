# Screenshot Endpoint (POST /api/v1/screenshot)

Captures a JPEG image of the Windows virtual desktop. AI callers must send the API token in the `Authorization` header and include a valid session. Human sessions are accepted by the local control page or a paired HTTPS client.

## Request Headers

- `Authorization`: `Bearer <token>` for AI sessions
- `Content-Type`: `application/json`

## Body Parameters

- `session`: UUID returned by `POST /api/v1/request-session` or the human session endpoint.
- `maxWidth`: optional integer from 320 to 3840; defaults to 1920.
- `quality`: optional JPEG quality from 30 to 90; defaults to 65.

```json
{
  "session": "<session-id>",
  "maxWidth": 1920,
  "quality": 65
}
```

## Responses

### 200 OK

- `Content-Type: image/jpeg`
- Binary JPEG response body.
- `X-Desktop-Width` and `X-Desktop-Height` contain the full virtual-desktop dimensions.
- `X-Desktop-Left` and `X-Desktop-Top` contain the virtual desktop's origin, including negative multi-monitor offsets.

The metadata lets clients translate positions on a resized image back to Windows desktop coordinates.

### 400 Bad Request

Invalid screenshot dimensions or JPEG quality.

### 401 Unauthorized

Missing/invalid session or Bearer header. Remote API requests also require HTTPS.
