# Keyboard (Capability)

> This is a capability, not an endpoint. To access it, see [Capability (/capability)](/guide/endpoints/capability).

Sends keypresses onto the host.

## Acceptable Keys

The following is a list of acceptable keys that can be passed to this capability as a key.

##### Alphanumeric Keys

* `a` to `z` + `shift` variants (e.g. `A`, `B`, `C`)
* `0` to `9` + `shift` variants (e.g. `!`, `@`, `$`)
* `numpad0` to `numpad9`
* `sp`, `space`

##### Extra Keys

* `` ` ``, `~`, `-`, `_`, `+`, `=`, `[`, `]`, `{`, `}`, `|`, `\`, `:`, `;`, `"`, `'`, `,`, `<`, `.`, `>`, `/`, `?`

##### Special Keys

* `enter`
* `bksp`, `backspace`
* `del`, `delete`
* `esc`, `escape`
* `tab`
* `cslk`, `capslock`
* `nmlk`, `numlock`
* `home`
* `end`
* `pgup`, `pageup`
* `pgdn`, `pagedown`
* `ins`, `insert`
* `prsc`, `printscreen`
* `sclk`, `scrolllock`
* `psbk`, `pausebreak`
* `f1` to `f24`

##### Modifier Keys

* `shift`, `lshift`
* `rshift`
* `ctrl`, `lctrl`
* `rctrl`
* `alt`, `lalt`
* `ralt`
* `meta`

##### Directional Keys

`up`, `down`, `left`, `right`

## Tasks

### 0: Keypress

Inputs a keypress on the host system.

#### Parameters

`key`: A key out of the acceptable keys to press.

`hold`: **OPTIONAL** How long to hold this key, in milliseconds. Default is **10ms**.

#### Returns

None

##### Example

```json
{
    "key": "sp",
    "hold": 500
}
```

### 1: Type

Types a sequence of keys on the host system.

#### Parameters

`text`: An array of keys out of the acceptable keys to type, or a string to type.

`delay`: **OPTIONAL** A delay between keypresses to allow the host to process them, in milliseconds. **Default is 5.**

`hold`: **OPTIONAL** How long to hold each key, in milliseconds. Default is **10ms**.

#### Returns

None

#### Example

```json
{
    "text": "tcpioneer",
    "hold": 500,
    "delay": 30
}
```

### 2: Type Shortcut

#### Parameters

`text`: An array of keys out of the acceptable keys, or a string, to press simultaneously.

`hold`: **OPTIONAL** How long to hold this shortcut, in milliseconds. Default is **5ms**.

> Shortcuts can be represented as a string by delimiting keys using `+`. For example: `ctrl+alt+del`

#### Returns

None

#### Example

```json
{
    "text": ["ctrl", "alt", "delete"],
    "hold": 200
}
```
