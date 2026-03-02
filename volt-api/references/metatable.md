# Metatable

Work with Lua metatables, including locked Roblox objects.

## Reading Metatables

### `getrawmetatable(obj): table`
Returns the metatable of `obj` even if `__metatable` would normally block `getmetatable()`. Works on Roblox instances.

## Writable Control

### `makewritable(obj)` — Make the metatable writable (allow modifications).
### `makereadonly(obj)` — Make it read-only again.
### `isreadonly(obj): boolean` — True if metatable is currently read-only.
### `iswritable(obj): boolean` — True if currently writable.
### `setreadonly(obj, state: boolean)` — Set read-only state directly.
### `setrawmetatable(obj, mt: table)` — Replace the object's metatable directly.

## Namecall Method

Useful inside `__namecall` hooks to identify which method is being called.

### `getnamecallmethod(): string`
Returns the method name being called via `:method()` syntax (only valid inside a `__namecall` hook).

### `setnamecallmethod(name: string)`
Override the namecall method name for the current call.

## Example: Intercepting `:FireServer`

```lua
local mt = getrawmetatable(game)
makewritable(mt)
local old__namecall = mt.__namecall
mt.__namecall = newcclosure(function(self, ...)
    local method = getnamecallmethod()
    if method == "FireServer" then
        local remote = self
        local args = {...}
        print("FireServer:", remote.Name, table.unpack(args))
    end
    return old__namecall(self, ...)
end)
```

## Common Metamethods

| Metamethod | Triggers when |
|---|---|
| `__index` | `obj.key` |
| `__newindex` | `obj.key = value` |
| `__namecall` | `obj:method()` |
| `__call` | `obj()` |
| `__tostring` | `tostring(obj)` |
| `__len` | `#obj` |
| `__eq` | `obj == other` |
