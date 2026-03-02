# Miscellaneous

Utility functions that don't fit other categories.

## HTTP Requests

### `request(options: table): table`
Aliases: `http.request`, `http_request`, `syn.request`

Perform an HTTP request. **Bypasses Roblox's HttpService restrictions.**

**Options table:**
| Field | Type | Description |
|---|---|---|
| `Url` | `string` | Request URL (required) |
| `Method` | `string` | `"GET"`, `"POST"`, `"PUT"`, `"DELETE"`, etc. (default: `"GET"`) |
| `Headers` | `{[string]: string}` | HTTP headers |
| `Body` | `string` | Request body (for POST/PUT) |
| `Cookies` | `{[string]: string}` | Cookies |

**Response table:**
| Field | Type | Description |
|---|---|---|
| `StatusCode` | `number` | HTTP status code |
| `StatusMessage` | `string` | Status text |
| `Success` | `boolean` | True if 2xx |
| `Headers` | `table` | Response headers |
| `Body` | `string` | Response body |

```lua
local res = request({
    Url = "https://api.example.com/data",
    Method = "POST",
    Headers = { ["Content-Type"] = "application/json" },
    Body = '{"key":"value"}'
})
if res.Success then
    print(res.Body)
end
```

## Game Saving

### `saveinstance(options?: table)`
Save the entire game to a `.rbxl` file in the workspace folder.

Options: `filepath`, `decompile`, `noscripts`, `scriptcachemode`

### `saveplace()`
Save the current place. Simpler alternative to `saveinstance`.

## Teleport Queue

### `queueonteleport(script: string)` — Execute a script after the next teleport.
### `clearqueueonteleport()` — Clear any queued teleport script.

## System Info

### `identifyexecutor(): (string, string)` — Returns executor name and version.
### `gethwid(): string` — Returns the hardware ID string.

## FPS

### `getfpscap(): number` — Current FPS cap.
### `setfpscap(fps: number)` — Set FPS cap override.

## Feature Flags

### `getfflag(name: string): string` — Get a Roblox FFlag value.
### `setfflag(name: string, value: string)` — Set an FFlag (must call before game loads).

## Misc

### `setclipboard(text: string)` — Copy text to OS clipboard.
### `messagebox(text: string, title: string, flags: number): number`
Show a Windows message box. Returns button ID pressed. Standard MB_* flags apply (0=OK, 1=OK+Cancel, 4=Yes+No, etc.).
