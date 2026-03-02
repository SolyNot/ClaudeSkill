# Closures

Inspect, hook, and create Luau closures.

## Closure Types

- **Luau closure** (`islclosure`): Written in Lua/Luau.
- **C closure** (`iscclosure`): Implemented in C (Roblox internals). Cannot be hooked with `hookfunction` — use `oth.hook` instead.
- **Executor closure** (`isexecutorclosure`): Created by Volt itself (via `newcclosure`/`newlclosure`).

## Inspection

### `islclosure(func): boolean` — Is it a Luau closure?
### `iscclosure(func): boolean` — Is it a C closure?
### `isexecutorclosure(func): boolean` — Created by executor?
### `isnewcclosure(func): boolean` — Created via `newcclosure`?
### `isfunctionhooked(func): boolean` — Currently hooked?
### `checkcaller(): boolean` — Is the current caller Volt (not game code)?
### `getfunctionhash(func): string` — Hash of the function's bytecode.

## Hooking

### `hookfunction(target, hook): originalFunction`
Replaces `target` with `hook`. Returns the original so you can call through. **Luau closures only** — for C closures use `oth.hook`.
```lua
local oldPrint = hookfunction(print, function(...)
    -- intercept all prints
    oldPrint("[HOOKED]", ...)
end)
```

### `hookmetamethod(object, metamethod: string, hook): originalFunction`
Hooks a metamethod on an object's (raw) metatable. Temporarily makes the metatable writable.
```lua
local oldIndex = hookmetamethod(game, "__namecall", function(self, ...)
    local method = getnamecallmethod()
    if method == "FireServer" then
        -- intercept RemoteEvent:FireServer
    end
    return oldIndex(self, ...)
end)
```

### `restorefunction(func)` — Remove hook, restore original.

## Creating Closures

### `newcclosure(func): cclosure` — Wraps a Luau function as a C closure (appears native).
### `newlclosure(func): lclosure` — Wraps a function as a new Luau closure.
### `clonefunction(func): function` — Creates an identical copy of a Luau closure.

## Stack Visibility

### `setstackhidden(func, hidden: boolean)` — Hide/show function in call stack traces.
