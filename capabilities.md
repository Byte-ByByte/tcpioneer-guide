# Capabilities

## Introduction

Capabilities define what interactions a client can operate on a host.

Currently supported capabilities in TCPIOneer include:

* **mouse**: Moving, clicking, dragging, and scrolling mouse inputs.
* **keyboard**: Pressing key combinations and typing unicode text strings.
* **screenshot**: Capturing resizable JPEG screenshots with native desktop coordinate metadata.
* **accessibility**: Returning a bounded Windows UI Automation tree with password fields masked.

## Available Actions

### Mouse
- `mouse.move`: Move cursor to `(x, y)` pixel coordinates.
- `mouse.click`: Perform `left`, `right`, or `middle` click.
- `mouse.drag`: Smoothly drag cursor from `(fromX, fromY)` to `(toX, toY)` holding `left`, `right`, or `middle` button.
- `mouse.scroll`: Scroll mouse wheel up or down by `amount`.

### Keyboard
- `keyboard.press`: Press key shortcut combinations (e.g., `["CTRL", "C"]`, `["WIN", "R"]`, `["ALT", "TAB"]`, `["ENTER"]`, `["ESC"]`).
- `keyboard.type`: Type unicode strings (up to 2,000 characters) directly into active input fields.

### Screenshot
- Captures the virtual desktop as JPEG, with configurable maximum width and quality.
- Returns full desktop size and origin in response headers so clients can map coordinates correctly.

### Accessibility
- Returns visible control names, roles, automation IDs, enabled state, bounds, and children.
- Limits the tree to 500 nodes and depth 8; password field values are never returned.
