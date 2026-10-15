# Run Capability (POST)

> This endpoint requires authentication. (see [Guide: Authentication](/guide#authentication))

> This endpoint requires a Session. (see [Guide: Session Lifecycle](/guide#session-lifecycle))

Requests the server to run a capability (see [Capabilities](/guide/capabilities)).

## Body Parameters

`Content-Type: JSON`

* `capability-name`: `string` Capability ID to run. See [Capabilities: Capabilities Table](/guide/capabilities#capabilities-table) for examples.
* `params`: `{...}` Parameters to the capability to run with. See [Capabilites: Capabilities Table](/guide/capabilities#capabilities-table) for specific documentation on each capability's parameters.
* `task` The task you want the capability to run. See [Capabilites: Capabilities Table](/guide/capabilities#capabilities-table) for specific documentation on each capability's tasks, and see [Capabilites: Tasks](/guide/capabilities#capabilities-table) for more information on tasks.
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

The resource the capability returned. See [Capabilites: Capabilities Table](/guide/capabilities#capabilities-table) for specific documentation on each capability's return value.

#### 404 Forbidden

##### Description:

Server policy prevents this capability or task from starting.

##### Returns:

An [error object](/guide/return-objects/error), which provides more error information.

### Responses inherited from: Authentication

#### 401 Unauthorized

The auth token provided was incorrect or absent.

### Responses inherited from: Session

#### 404 Not Found

##### Description:

The session key does not exist or is incorrect.

##### Returns:

An [error object](/guide/return-objects/error), which provides more error information.

#### 410 Gone

##### Description:

The requested session key has been deleted.

> **This error can only be emitted once per session key; the subsequent request for the session key after its deletion.** Once you recieve this error, you **must** not attempt to use this session key again. (see [Guide: Session Deletion](/guide#session-deletion))

##### Returns:

An [error object](/guide/return-objects/error), which provides more error information.

#### 404 Not Found

### Responses inherited from: Server Side Errors

#### 500 Internal Server Error

##### Description:

An error has occured within a capability, or an issue has happened internally with the TCPIOneer host. This is usually not the client's fault.

##### Returns:

An [error object](/guide/return-objects/error), which provides more error information.