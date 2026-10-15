# Error Object

The error object provides extra information about an error through JSON.

In this document is a:

* Typing of the error object
* Description of each property
* Example of a loaded error object

## Typing

Attributes for the error object are listed as:

* `code`: `string`, error code of an error. Can only be an error code listed in [Error Codes: Codes](/guide/error-codes#codes).
* `message`: `string`, user-facing message of an error code. Can only be an error message listed in [Error Codes: Codes](/guide/error-codes#codes).
* `source`: `"server" | "client"` Which side of the server-client boundary **caused** the  error.
* `extra-info`: `{ ... }` Error-specific information, more info listed at [Error Codes: Codes](/guide/error-codes#codes).

## Examples

### Fully loaded example

Below is an example error object that is fully filled out.

```json
{
    "code": "SESSION_NOT_FOUND",
    "message": "The session could not be found.",
    "source": "server",
    "extra-info": {}
}
```

### TypeScript typing

Below is a fully compatible TypeScript type that can be dropped into code without modification.

```typescript
type SessionObject = {
    "code": string
    "message": string
    "source": "server" | "client"
    "extra-info": {}
}
```