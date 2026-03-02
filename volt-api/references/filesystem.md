# Filesystem

Read, write, and manage files. All paths are **relative to Volt's sandboxed workspace folder**.

## Files

### `readfile(path: string): string`
Read file contents as a string.

### `writefile(path: string, content: string)`
Write (overwrite) a file. Creates parent folders if needed.

### `appendfile(path: string, content: string)`
Append content to an existing file.

### `delfile(path: string)`
Delete a file.

### `isfile(path: string): boolean`
Returns `true` if path is an existing file.

### `loadfile(path: string): (function?, string?)`
Load and compile a Lua file as a chunk. Returns `(func, nil)` on success or `(nil, error)`.
```lua
local fn, err = loadfile("myscript.lua")
if fn then fn() else warn(err) end
```

### `dofile(path: string)`
Load and immediately execute a file.

### `getcustomasset(path: string): string`
Returns an `rbxasset://` URI for a file in the workspace, usable with `Image` drawing objects and UI.

## Folders

### `makefolder(path: string)` — Create a directory (and parents).
### `delfolder(path: string)` — Delete a directory.
### `isfolder(path: string): boolean` — True if path is a directory.
### `listfiles(path: string): {string}` — List all files/folders in directory.

## Example

```lua
-- Save config
local config = { speed = 10, jump = true }
writefile("myscript/config.json",
    game:GetService("HttpService"):JSONEncode(config))

-- Load it back
if isfile("myscript/config.json") then
    local data = readfile("myscript/config.json")
    config = game:GetService("HttpService"):JSONDecode(data)
end

-- List workspace root
for _, name in ipairs(listfiles("")) do
    print(name)
end
```
