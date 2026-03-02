# Input

Simulate keyboard and mouse input at the OS level.

## Window

### `iswindowactive(): boolean`
Returns `true` if the Roblox window is currently focused.

## Keyboard

### `keypress(keycode: number)` — Hold a key down.
### `keyrelease(keycode: number)` — Release a held key.
### `keyclick(keycode: number)` — Press and release a key (combines press + release).

Use Windows Virtual Key codes (e.g. `0x41` = A, `0x0D` = Enter, `0x20` = Space).

```lua
-- Press and release the F key
keyclick(0x46)
```

## Mouse Buttons

### `mouse1press()` — Hold left mouse button.
### `mouse1release()` — Release left mouse button.
### `mouse1click()` — Left click (press + release).
### `mouse2press()` — Hold right mouse button.
### `mouse2release()` — Release right mouse button.
### `mouse2click()` — Right click.

## Mouse Movement

### `mousemoverel(dx: number, dy: number)` — Move mouse by relative offset from current position.
### `mousemoveabs(x: number, y: number)` — Move mouse to absolute screen coordinates.
### `mousescroll(delta: number)` — Scroll mouse wheel. Positive = up, negative = down.

## Example

```lua
-- Click at a specific screen position
mousemoveabs(960, 540)
task.wait(0.05)
mouse1click()
```
