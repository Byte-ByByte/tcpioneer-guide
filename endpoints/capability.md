# Run Capability (POST)

> This endpoint requires authentication. (see [Guide: Authentication](/guide#authentication))

> This endpoint requires a Session. (see [Guide: Session Lifecycle](/guide#session-lifecycle))

Requests the server to run a capability (see [Capabilities](/guide/capabilities)).

## Body Parameters

`Content-Type: JSON`

* `capability-name`: `string` Capability ID to run. See [Capabilities: Capabilities Table](/guide/capabilities#capabilities-table) for examples.
* `params`: `{...}` Parameters to the capability to run with. See [Capabilites: Capabilities Table](/guide/capabilities#capabilities-table) for specific documentation on each capability's parameters.
* `session`: Inherited from [Guide: Session Usage](/guide#session-usage). The session key you want this capability to be used on.


## Examples

```http

```

## Headers

### Headers inherited from: Authentication

`Authorization`: `Bearer` token that matches the server's token (see [Guide: Authentication](/guide#authentication)).

## Responses

#### 200 OK

##### Description:

The interaction completed successfully.

##### Returns:

None

### Responses inherited from: Authentication

#### 401 Unauthorized

The auth token provided was incorrect or absent.

### Responses inherited from: Server Side Errors

#### 500 Internal Server Error

##### Description:

An issue has happened internally with the TCPIOneer host. Inform an admin if this is a recurring issue.

##### Returns:

None