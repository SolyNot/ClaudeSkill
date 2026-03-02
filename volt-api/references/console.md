# Console

Custom debug console window management.

## Window Control

| Function | Description |
|---|---|
| `rconsoleshow()` | Show the console window |
| `rconsolehide()` | Hide the console window |
| `rconsoletoggle()` | Toggle visibility |
| `rconsolehidden(): boolean` | Returns `true` if hidden |
| `rconsoletop(bool)` | Set always-on-top |
| `rconsolename(title: string)` | Set window title |

## Output

| Function | Description |
|---|---|
| `rconsoleprint(text: string)` | Print plain text |
| `rconsoleinfo(text: string)` | Print info-styled line |
| `rconsolewarn(text: string)` | Print warning-styled line |
| `rconsoleerr(text: string)` | Print error-styled line |
| `rconsoleclear()` | Clear all console output |

## Input

### `rconsoleinput(): string`
Blocks until the user types something and presses Enter; returns the input string.
```lua
rconsoleshow()
rconsolename("My Script")
rconsoleprint("Enter your name: ")
local name = rconsoleinput()
rconsoleprint("Hello, " .. name)
```
