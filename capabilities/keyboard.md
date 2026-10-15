# Keyboard (Capability)

> This is a capability, not an endpoint. To access it, see [Capability (/capability)](/guide/endpoints/capability).

Sends keypresses onto the host and can tramsmit recent keypresses from the host.

> Note: **Not all recent keypresses are returned by this capability for security reasons.** The host can choose which recent keypresses to return, to clear keypress history, or to only show keypresses between a certain time or date.

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

* `lshift`, `rshift`
* `lctrl`, `rctrl`
* `lalt`, `ralt`
* `meta`

##### Directional Keys

`up`, `down`, `left`, `right`

## Tasks

### 0: Keypress

Inputs a keypress on the host system.

#### Parameters

`key`: A key out of the acceptable keys to press.

### 1: Type

Types a sequence of keys on the host system.

#### Parameters

`keys`: An array of keys out of the acceptable keys to type, or a string to type.

`delay`: **OPTIONAL** A delay between keypresses to allow the host to process them, in milliseconds. **Default is 5.**

#### Returns

None

### 2: Type Shortcut

#### Parameters

`keys`: An array of keys out of the acceptable keys to press as a shortcut.

#### Returns

None

### 3: Fetch Last Keypresses

#### Parameters

`length`: **OPTIONAL** The amount of keypresses you want to fetch from the host. This is **best-effort** for security. **Default is maximum.**

#### Returns

Array of keypresses in 